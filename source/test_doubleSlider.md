---
title: test_doubleSlider
date: 2020-05-07
---
Example Python program test_doubleSlider.py

## Modules

* from unittest import TestCase
* from PyQt5.QtWidgets import QSlider
* from DoubleSlider import DoubleSlider

## Classes

* class TestDoubleSlider(TestCase):

## Methods

* def setUp(self):
* def test_if_double_slider_is_subclass_of_QSlider(self):
* def test_set_float_value(self):
* def test_default_min_max_values(self):
* def test_setting_minimum_value_above_maximum_value(self):
* def test_setting_maximum_value_below_minimum_value(self):
* def test_valid_limits(self):
* def test_setting_value_below_lower_limit(self):
* def test_setting_value_above_upper_limit(self):
* def test_usual_numbers(self):
* def test_negative_range(self):

## Code

Example Python PyQt program :

    from unittest import TestCase
    from PyQt5.QtWidgets import QSlider
    from DoubleSlider import DoubleSlider
    
    class TestDoubleSlider(TestCase):
        def setUp(self):
            self.slider = DoubleSlider()
    
        def test_if_double_slider_is_subclass_of_QSlider(self):
            self.assertIsInstance(self.slider, QSlider)
    
        def test_set_float_value(self):
            self.slider.setValue(0.0)
            self.assertAlmostEqual(self.slider.value(), 0.0, delta=0.01)
    
            self.slider.setValue(0.6)
            self.assertAlmostEqual(self.slider.value(), 0.6, delta=0.01)
    
        def test_default_min_max_values(self):
            self.assertAlmostEqual(self.slider.minimum(), 0.0, delta=0.001)
            self.assertAlmostEqual(self.slider.maximum(), 1.0, delta=0.001)
    
        def test_setting_minimum_value_above_maximum_value(self):
            with self.assertRaises(ValueError):
                self.slider.setMinimum(2.0)
    
        def test_setting_maximum_value_below_minimum_value(self):
            with self.assertRaises(ValueError):
                self.slider.setMaximum(-0.5)
    
        def test_valid_limits(self):
            self.slider.setMinimum(0.6)
            self.slider.setMaximum(2.3)
            self.assertAlmostEqual(self.slider.minimum(), 0.6, delta=0.001)
            self.assertAlmostEqual(self.slider.maximum(), 2.3, delta=0.001)
    
            self.slider.setMinimum(-5.0)
            self.slider.setMaximum(-2.0)
            self.assertAlmostEqual(self.slider.minimum(), -5.0, delta=0.001)
            self.assertAlmostEqual(self.slider.maximum(), -2.0, delta=0.001)
    
        def test_setting_value_below_lower_limit(self):
            self.slider.setMinimum(0.6)
            self.slider.setValue(0.2)
            self.assertAlmostEqual(self.slider.value(), 0.6, delta=0.001)
    
        def test_setting_value_above_upper_limit(self):
            self.slider.setMaximum(0.6)
            self.slider.setValue(0.9)
            self.assertAlmostEqual(self.slider.value(), 0.6, delta=0.001)
    
        def test_usual_numbers(self):
            self.slider.setMinimum(0.8)
            self.slider.setMaximum(2.3)
            self.slider.setValue(1.46)
            self.assertAlmostEqual(self.slider.value(), 1.46, delta=0.01)
    
        def test_negative_range(self):
            self.slider.setMinimum(-5.0)
            self.slider.setMaximum(-1.0)
            self.slider.setValue(-4.4)
            self.assertAlmostEqual(self.slider.value(), -4.4, delta=0.01)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
