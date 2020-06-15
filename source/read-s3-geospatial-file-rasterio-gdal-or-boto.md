---
title: read s3 geospatial file rasterio gdal or boto
date: 2020-05-07
---
Example Python program read-s3-geospatial-file-rasterio-gdal-or-boto.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import rasterio
* from osgeo import gdal
* import boto3
* from io import BytesIO
* import matplotlib.image as mpimg
* import matplotlib.pyplot as plt

## Code

Python example

    # Open S3 with Rasterio
    import rasterio
    
    s3uri = 's3://mapbox/rasterio/shade.tif'
    with rasterio.open(s3uri) as dataset:
        print(dataset.bounds, dataset.count, dataset.indexes) 
        band1 = dataset.read(1) 
        print(band1)
    
    
    # Open S3 with GDAL only
    # Need GDAL 2.3+
    # export AWS_SECRET_ACCESS_KEY="TRUE"
    from osgeo import gdal
    
    # For s3 streaming, use '/vsis3_streaming/' instead of '/vsis3/'
    ds = gdal.Open(s3uri.replace('s3://', '/vsis3/'))
    
    print(ds.RasterCount)
    srcband = ds.GetRasterBand(1)
    print(srcband)
    
    
    # Pure python (no geospatial library)
    # There more alternative depending wether you want to manipulate image in 
    # memory or write it
    import boto3
    from io import BytesIO
    import matplotlib.image as mpimg
    import matplotlib.pyplot as plt
    
    resource = boto3.resource('s3')
    bucket = resource.Bucket('mapbox')
    
    image_object = bucket.Object('rasterio/shade.tif')
    image = mpimg.imread(BytesIO(image_object.get()['Body'].read()), 'tif')
    
    plt.figure(0)
    plt.imshow(image)
    plt.savefig('shade.png')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
