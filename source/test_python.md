---
title: test_python
date: 2020-05-07
---
Example Python program test_python.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import unittest
* import glob
* from src.utils import load_img
* from modules import AestheticFea
* from modules import GarmentDetector
* from modules import ColorConsist

## Classes

* class TestModule(unittest.TestCase):

## Methods

* def setUp(self):
* def test_detector(self):
* def test_colorconsis(self):
* def test_aesthetic(self):
* def tearDown(self):

## Code

Python example

    """
    This is the test script;
    """
    import os
    os.environ['CUDA_VISIBLE_DEVICES'] = '-1'
    
    import sys
    sys.path.append('.')
    
    import unittest
    import glob
    from src.utils import load_img
    
    from modules import AestheticFea
    from modules import GarmentDetector
    from modules import ColorConsist
    
    class TestModule(unittest.TestCase):
        def setUp(self):
            print('Start test the aesthetic feature module!')
    
        def test_detector(self):
            detector = GarmentDetector()
            sku_folder = 'test_scripts/samples/29509596057/'
            image_paths = glob.glob(f"{sku_folder}/*.jpg")
            image_paths.sort()
            image_inputs = [load_img(img_path) for _,img_path in enumerate(image_paths)]
            detect_results = detector.predict_ondata([image_inputs[0]])
            self.assertTrue(len(detect_results) > 0)
            
        def test_colorconsis(self):
            sku_folder = 'test_scripts/samples/29509596057/'
            image_paths = glob.glob(f"{sku_folder}/*.jpg")
            image_paths.sort()
            image_inputs = [load_img(img_path) for _,img_path in enumerate(image_paths)]
            self.colorconsis = ColorConsist()
            self.colorconsis.load_model()
            self.colorconsis.update_data(image_inputs)
            res = {}
            self.colorconsis.predict(res)
            self.assertTrue(res['colorconsis_res']>0)
    
        def test_aesthetic(self):
            sku_folder = 'test_scripts/samples/29509596057/'
            image_paths = glob.glob(f"{sku_folder}/*.jpg")
            image_paths.sort()
            image_inputs = [load_img(img_path) for _,img_path in enumerate(image_paths)]
            detector = GarmentDetector()
            detect_results = [detector.predict_ondata([img_data]) for img_data in image_inputs]
            self.aestheticFeaEx = AestheticFea()
            self.aestheticFeaEx.load_model()
            self.aestheticFeaEx.update_data([image_inputs,detect_results])
            self.assertEqual(len(self.aestheticFeaEx.img_dect), 3)
            self.assertEqual(len(self.aestheticFeaEx.img_data), 3)
    
            res = {}
            self.aestheticFeaEx.predict(res)
            self.assertTrue(res['aesthetic_res']>0)
            
        def tearDown(self):
            print('tear Down')
    
    if __name__ == "__main__":
       unittest.main() 

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
