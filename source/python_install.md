---
title: python_install
date: 2020-05-07
---
Example Python program python_install.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os, requests, shutil
* import sh
* from fenx.tools.process_output import logger, steps
* from fenx.tools.utils import sudo, download_file, OS, copytree, move_tree, is_admin
* from fenx.tools import qt_cmd, utils

## Methods

* def install(install_dir, version=2, requirements=None, percentages=None, temp_dir=None, sudopwd=None):
* def install_requirements(python_root, requirements, percentages=None):
* def execute_command(cmd):

## Code

Python example

    import os, requests, shutil
    try:
        import sh
    except:
        pass
    from fenx.tools.process_output import logger, steps
    from fenx.tools.utils import sudo, download_file, OS, copytree, move_tree, is_admin
    requests.packages.urllib3.disable_warnings()
    from fenx.tools import qt_cmd, utils
    # PY_VERSION = 20168704
    PY2_URL = 'https://www.python.org/ftp/python/2.7.14/python-2.7.14.amd64.msi'    #todo: get last version
    # PY3_URL = 'https://www.python.org/ftp/python/3.6.4/python-3.6.4-amd64.exe'            #todo: get last version
    # PY3_URL = 'https://www.python.org/ftp/python/3.6.4/python-3.6.4-embed-amd64.zip'      #todo: get last version
    PY3_URL = 'https://netix.dl.sourceforge.net/project/winpython/WinPython_3.6/3.6.3.0/WinPython-64bit-3.6.3.0Zero.exe'      #todo: get last version
    PY2_GET_PIP_URL = "https://raw.githubusercontent.com/pypa/get-pip/master/get-pip.py"
    
    
    def install(install_dir, version=2, requirements=None, percentages=None, temp_dir=None, sudopwd=None):
        # qcmd = qt_cmd.Cmd()
        if percentages:
            if requirements:
                pr1 = percentages[0], percentages[0] + ((percentages[1] - percentages[0]) / 2)
                pr2 = percentages[1] - ((percentages[1] - percentages[0]) / 2), percentages[1]
            else:
                pr1 = percentages
                pr2 = None
        else:
            pr1 = None
            pr2 = None
        result = {}
        py_dir = os.path.normpath(os.path.join(install_dir, 'python'))
        print( 'Install Python {} to {}'.format(version, py_dir))
        if OS.is_windows():
            with steps(5, pr1, logger.progress, 1) as st:
                # ============ WINDOWS
                st.step()
                py_exe = os.path.join(py_dir, 'python.exe')
                if os.path.exists(py_exe):
                    logger.log('Python already installed.')
                    return py_exe
                py_installer = download_file(PY2_URL if version == 2 else PY3_URL, temp_dir=temp_dir)
                if not py_installer:
                    logger.error('File not downloaded')
                    return
                st.step()
                if not os.path.exists(py_installer):
                    logger.error('File not exists: {}'.format(py_installer))
                    return
                if version == 2:
                    # ============ PYTHON 2
                    py_install_cmd = 'start /wait msiexec /a "{local_py}" /qb TARGETDIR="{install_dir}"'.format(
                        local_py=os.path.normpath(py_installer),
                        install_dir=py_dir
                    )
                    # logger.log('Install Python {} to {}...'.format(version, install_dir))
                    # os.system(py_install_cmd)
                    # qcmd._call(py_install_cmd)
                    execute_command(py_install_cmd)
                    st.step()
                    if not os.path.exists(py_exe):
                        logger.error('Python installation failed. {} not found'.format(py_exe))
                        return
                    result['py_exe'] = py_exe
                    logger.log('Python installed: {}'.format(py_exe))
                    # os.system('{} -V'.format(py_exe))
                    execute_command('{} -V'.format(py_exe))
                    # qcmd._call('{} -V'.format(py_exe))
                    st.step()
                    # INSTALL PIP
                    logger.log('Install PIP')
                    pip_exe = os.path.exists(os.path.join(py_dir, 'Scripts', 'pip.exe'))
                    if not os.path.exists(pip_exe):
                        get_pip_script = download_file(PY2_GET_PIP_URL, temp_dir=temp_dir)
                        if get_pip_script:
                            # os.system(' '.join([py_exe, get_pip_script]))
                            # qcmd._call(' '.join([py_exe, get_pip_script]))
                            execute_command(' '.join([py_exe, get_pip_script]))
                        else:
                            logger.error('get-pip.py not found')
                            return
                        pip_exe = os.path.join(py_dir, 'Scripts', 'pip.exe')
                        if not os.path.exists(pip_exe):
                            logger.error('pip not installed')
                            return
                    st.step()
                    result['pip_exe'] = pip_exe
                else:
                    # ============ PYTHON 3
                    # default python
                    # py_install_cmd = 'START /WAIT {local_py} /quiet InstallAllUsers=1 Include_tcltk=0 TargetDir={install_dir} AssociateFiles=0 Include_doc=0'.format(
                    #     local_py=os.path.normpath(py_installer),
                    #     install_dir=os.path.normpath(install_dir)
                    # )
                    install_tmp_dir = os.path.join(temp_dir, 'tmp_py3')
                    if not os.path.exists(install_tmp_dir):
                        try:
                            os.makedirs(install_tmp_dir)
                        except:
                            logger.error('Can\'t create temp folder:'.format(install_tmp_dir))
                            return
                    logger.log('Extracting...')
                    py_install_cmd = 'START /WAIT {local_py} /S /D={install_dir}'.format(
                    # py_install_cmd = 'START /WAIT {local_py} /S /D={install_dir}'.format(
                        local_py=os.path.normpath(py_installer),
                        install_dir=os.path.normpath(install_tmp_dir)
                    )
    
                    st.step()
                    # logger.log(py_install_cmd)
                    os.system(py_install_cmd)
                    # qcmd._exec(py_install_cmd)
    
                    tmp_py_dir = ([os.path.join(install_tmp_dir, x) for x in os.listdir(install_tmp_dir) if
                               os.path.exists(os.path.join(install_tmp_dir, x, 'python.exe'))] or [None])[0]
                    if not tmp_py_dir:
                        logger.error('Python installation failed. Python.exe not found: {}'.format(tmp_py_dir))
                        return
                    st.step()
                    logger.log('Move files...')
                    try:
                        # os.rename(py_dir, install_dir)
                        copytree(tmp_py_dir, py_dir)
                        # print(move_tree(tmp_py_dir, py_dir))
                    except Exception as e:
                        print(str(e))
                        logger.error('Python installation failed. Can\'t rename installed dir. "{}" > "{}"'.format(tmp_py_dir, py_dir))
                        return
                    try:
                        shutil.rmtree(install_tmp_dir)
                    except:
                        logger.log('Can\'t remove temp dir: {}'.format(install_tmp_dir))
                    st.step()
                    pip_exe = os.path.join(py_dir, 'puthon.exe') + '-mpip'
                    result['pip_exe'] = pip_exe
            # return result
        elif OS.is_linux():
            if not is_admin():
                logger.error('Need sudo permissions for install. '
                             'You can install python and libs manually and restart installer:'
                             ' sudo apt-get install python-dev python-pip libpq-dev python-pyside')
                raise Exception('Require SUDO privileges')
            # ============== LINUX
            with steps(4, pr1, logger.progress, 1) as st:
                ve_exists = sh.which('virtualenv')
                # py_exists = sh.which('python') if version == 2 else sh.which('python3.6')
                py36 = '/usr/bin/python3.6'
                py_exists = py36 if os.path.exists(py36) else ''
                st.step()
                if version == 2:
                    # ================= PYTHON 2
                    # install python if not exists
                    if not os.path.exists('/usr/bin/python2'):
                        logger.error('System python 2 not installed')
                        return
                    # install lib and pip
                    sudo('apt-get -y install python-dev python-pip libpq-dev python-pyside', sudopwd)
                    st.step()
                    # virtual env
                    if not ve_exists:
                        sudo('pip install virtualenv', sudopwd)
                        # create env
                    logger.log('Create virtual env...')
                    sh.cd(install_dir)
                    sh.virtualenv(os.path.basename(py_dir), '--no-site-packages')
                    st.step()
                    py_exe = os.path.join(install_dir, 'bin', 'python')
                    result['py_exe'] = py_exe
                    pip_exe = os.path.join(install_dir, 'bin', 'pip')
                    result['pip_exe'] = pip_exe
                    # env_exe = os.path.join(install_dir, 'bin', 'activate')
                    # result['env_exe'] = env_exe
                    # sh.source(install_dir)
                    # PySide
                    site_packages = os.path.join(install_dir, 'lib', 'python2.7', 'site-packages')
                    default_pyside = '/usr/lib/python2.7/dist-packages/PySide'
                    if os.path.exists(default_pyside):
                        copytree(default_pyside, os.path.join(site_packages, 'PySide'))
                    else:
                        logger.error('PySide not installed')
                        return
                    st.step()
                else:
                    # PYTHON 3
                    lines =[]
                    if not os.path.exists(py_exists):
                        lines +=[
                            'add-apt-repository -y ppa:jonathonf/python-3.6',
                            'apt-get update',
                        ]
                    lines += ['apt-get install -y build-essential libssl-dev libffi-dev python3-dev']
                    if not sh.which('pip3'):
                        lines += [
                            'apt-get install -y python3.6 python3-pip',
                            'pip3 install --upgrade pip',
                        ]
                    if not os.path.exists('/usr/lib/python3.6/venv'):
                        lines.append('apt-get install -y python3-venv')
                        lines.append('apt-get install -y python3.6-venv')
                    if not lines:
                        print('No commands to execute')
                    for line in lines:
                        print('>>', line)
                        sudo(line, sudopwd)
                    st.step()
                    # v = sh.python3('-V').strip().split(' ')[-1][:3]
                    # sudo('update-alternatives --install /usr/bin/python3 python3 /usr/bin/python{} 3'.format(v), sudopwd)
                    # ''''#update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 3'''
    
                    # create virtualenv
                    print('Create virtualenv')
                    if not os.path.exists(install_dir):
                        os.makedirs(install_dir)
                    sh.cd(install_dir)
                    print('go to {}'.format(install_dir))
                    cmd ='{} -m venv {}'.format(py_exists, os.path.basename(py_dir))
                    print(cmd)
                    sudo(cmd)
                    py_exe = os.path.join(py_dir, 'bin', 'python')
                    result['py_exe'] = py_exe
                    if not os.path.exists(py_exe):
                        logger.error('Python binary not found: {}'.format(py_exe))
                        return
                    st.step()
                    pip_exe = os.path.join(py_dir, 'bin', 'pip3')
                    # os.system('{} install --upgrade pip'.format(pip_exe))
                    # qcmd._call('{} install --upgrade pip'.format(pip_exe))
                    execute_command('{} install --upgrade pip'.format(pip_exe))
                    result['pip_exe'] = pip_exe
                    st.step()
                    # https://losst.ru/ustanovka-python-3-ubuntu
        elif OS.is_mac():
            # https://wsvincent.com/install-python3-mac/
            logger.error('OS X not supported yet')
            return
        else:
            logger.error('OS not supported yet')
            return
        # REQUIREMENTS
        logger.log('Install requirements...')
        if requirements:
            # print('='*10, requirements)
            install_requirements(py_dir, requirements, pr2)
        return result
    
    
    def install_requirements(python_root, requirements, percentages=None):
        # qcmd = qt_cmd.Cmd()
        if OS.is_windows():
            pip_exe = os.path.join(python_root, 'python.exe') + ' -mpip'
        elif OS.is_linux():
            pip_exe = os.path.join(python_root, 'bin', 'pip')
        elif OS.is_mac():
            pip_exe = os.path.join(python_root, 'bin', 'pip')
        else:
            raise Exception('Unknown OS!!!')
    
        for pkg in steps(requirements, percentages, logger.progress, 1):
            requirements_cmd = ' '.join([pip_exe, 'install', pkg])
            print(' '.join([pip_exe, 'install', pkg]))
            # os.system(requirements_cmd)
            # print(pkg)
            # qcmd._call(pip_exe, 'install', pkg)
            # utils.call(' '.join([pip_exe, 'install', pkg]))
            execute_command(requirements_cmd)
    
    
    def execute_command(cmd):
        # os.system(cmd)
        # qt_cmd.Cmd()._call(cmd)
        utils.call(cmd)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
