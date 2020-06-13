---
title: docker_example
date: 2020-05-07
---
Example Python program docker_example.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import tarfile
* import json
* import warnings
* from io import BytesIO
* from docker import Client
* from docker.utils import kwargs_from_env, create_host_config
* from __future__ import unicode_literals
* import os
* import redis

## Methods

* def docker_pull(image):
* def pull_dependencies():
* def clean_existing_containers():
* def generate_tarball_with_application(TARBALL_DESTINATION_NAME='python_application.tar.gz'):
* def build_docket_image_with_python_application(tag='testing-redis'):
* def main():

## Code

Python example

    import tarfile
    import json
    import warnings
    # This is just a very simple example of 2 cool things that you can do in python:
    # * Control the docker daemon, pushing files to it, building and running docker images
    # * Creating tarballs in pure python
    
    from io import BytesIO
    try:
        from docker import Client
        from docker.utils import kwargs_from_env, create_host_config
    except ImportError:
        print "First, install docker-py: pip install docker-py"
        raise SystemExit(1)
    
    warnings.simplefilter("ignore")
    
    kwargs = kwargs_from_env()
    kwargs['tls'].verify = False
    kwargs['timeout'] = 60 * 5
    docker = Client(**kwargs)
    
    dependency_images = ['ubuntu:latest', 'redis:latest']
    
    
    def docker_pull(image):
        for line in docker.pull(image, stream=True):
            print "docker pull redis:latest"
            json.dumps(json.loads(line), indent=4)
    
    
    def pull_dependencies():
        for image in dependency_images:
            docker_pull(image)
    
    
    def clean_existing_containers():
        # equivalent to
        # docker stop $(docker ps -aq)
        # docker rm -f $(docker ps -aq)
        for container in docker.containers(all=True):
            print "cleaning up", container['Image'], container['Id']
            docker.stop(container['Id'])
            docker.remove_container(container['Id'], force=True)
    
    
    def generate_tarball_with_application(TARBALL_DESTINATION_NAME='python_application.tar.gz'):
        # Given a python script that sets some keys in redis, then retrieves
        # them right away and prints them
        PYTHON_SCRIPT = '''#!/usr/bin/env python
    # -*- coding: utf-8 -*-
    #
    from __future__ import unicode_literals
    import os
    import redis
    
    
    conn = redis.Redis(os.environ["REDIS_HOST"])
    
    print "SET foo bar"
    conn.set("foo", "bar")
    conn.set("chuck", "norris")
    print "KEYS *"
    
    print ", ".join(conn.keys())
    
    for key in conn.keys():
        print "GET", key
        print conn.get("foo")
    '''
    
        # And given a Dockerfile that install python2.7 and pip in a brand
        # new ubuntu environment
        DOCKERFILE = '''FROM ubuntu:latest
    RUN apt-get update \
      && apt-get --yes --no-install-recommends install \
        python2.7 \
        wget \
        python-pip \
      && rm -rf /var/lib/apt/lists/*
    
    RUN chmod +x predis.py
    RUN pip install redis
    
    CMD ["python", "predis.py"]
    '''
    
        # When I get in-memory file objects with the those scripts above
        filesystem = [
            ('predis.py', PYTHON_SCRIPT),
            ('Dockerfile', DOCKERFILE),
        ]
        tarball = tarfile.TarFile(TARBALL_DESTINATION_NAME, "w")
    
        for file_name, file_contents in filesystem:
            fd = BytesIO(file_contents.encode('utf-8'))
            info = tarfile.TarInfo(name=file_name)
            info.size = len(file_contents)
            tarball.addfile(tarinfo=info, fileobj=fd)
    
        tarball.close()
        return open(TARBALL_DESTINATION_NAME, 'rb')
    
    
    def build_docket_image_with_python_application(tag='testing-redis'):
        print "docker build -t {0}".format(tag)
        docker_build = [json.loads(l) for l in docker.build(
            fileobj=generate_tarball_with_application(),
            rm=True,
            forcerm=True,
            nocache=True,
            tag=tag,
            custom_context=True,
            encoding='gzip',
        )]
        return docker_build
    
    
    def main():
        clean_existing_containers()
        pull_dependencies()
    
        # print docker build output in yellow, just because...
        for line in build_docket_image_with_python_application():
            print "\033[1;33m{0}\033[0m".format(line)
    
        redis = docker.create_container(
            image='redis:latest',
            name='redis1',
            detach=True,
            hostname='redis1')
    
        docker.start(redis['Id'])
    
        redis_python_app = docker.create_container(
            detach=True,
            image='testing-redis',
            environment={
                'REDIS_HOST': 'roundhousekick'
            },
            host_config=create_host_config(
                links=[
                    ('redis1', 'roundhousekick')
                ]
            ),
            name='test1',
        )
    
        docker.start(redis_python_app['Id'])
        # print the output in green, because green is beautiful, green is good !!!!
        for line in docker.logs(redis_python_app['Id'], stream=True, stdout=True):
            print "\033[1;32m{0}\033[0m".format(line.rstrip('\n'))
    main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
