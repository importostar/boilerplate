---
title: weather (1)
date: 2020-05-07
---
Example Python program weather (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import requests
* import sys
* from PyQt5 import QtCore
* from PyQt5.QtWidgets import QApplication, QWidget
* from gui import Ui_main
* import configparser as cp

## Classes

* class Main(QWidget):

## Methods

* def test_connection(forecast_url, current_url):
* def display_current(current_url):
* def display_forecast(forecast_url, days):
* def __init__(self):
* def refresh_current(self):
* def refresh_forecast(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    
    '''Weather desktop widget, fetches current weather from weather underground and
       displays current forecast and 0-2 days of 10 day forecast.'''
    
    
    import requests
    import sys
    from PyQt5 import QtCore
    from PyQt5.QtWidgets import QApplication, QWidget
    from gui import Ui_main
    import configparser as cp
    
    
    def test_connection(forecast_url, current_url):
        try:
            (requests.get(forecast_url).json()['forecast']['simpleforecast']
             ['forecastday'])
            requests.get(current_url).json()['current_observation']
        except:
            print('Could not connect to WeatherUnderground.')
    
    
    def display_current(current_url):
        current = requests.get(current_url).json()['current_observation']
        display_location = current['display_location']['full']
        update_time = current['observation_time']
        condition = current['weather']
        temp = current['temp_f']
        temp_feelslike = current['feelslike_f']
        wind_chill = current['windchill_f']
        humidity = current['relative_humidity']
        wind_dir = current['wind_dir']
        wind_speed = current['wind_mph']
        icon_url = current['icon_url'].split('/')[-1]
    
        html = r'''
    <!DOCTYPE html>
    <html>
    <head>
        <title></title>
    </head>
    <body>
        <div align="right"><img src="img/wu_logo.gif"></div>
        <center>
            <font size="4"><b>{}</b></font><br>
            <font size="2">{}</font>
        </center>
        <font size="1">
        <table style="width:100%">
            <tr>
                <td><b>Temperature:</b> {}°F<br>
                <b>Feels like:</b> {}°F<br>
                <b>Wind Chill:</b> {} °F<br>
                <b>Humidity:</b> {} in<br>
                <b>Wind:</b> {}mph {}<br></td>
                <td>
                    <div align="left">
                        <b>Conditions:</b> {}
                    </div>
                    <center>
                        <img src="img/{}">
                    </center>
                </td>
            </tr>
        </table>
        </font>
    </body>
    </html>
    '''.format(display_location, update_time, temp, temp_feelslike, wind_chill,
               humidity, wind_speed, wind_dir, condition, icon_url)
        return html
    
    
    def display_forecast(forecast_url, days):
        forecast = (requests.get(forecast_url).json()['forecast']['simpleforecast']
                    ['forecastday'])
        weekday = forecast[days]['date']['weekday']
        if days == 0:
            weekday = 'Today'
        condition = forecast[days]['conditions']
        condition_icon = forecast[days]['icon_url']
        condition_icon = condition_icon.split('/')[-1]
        temp_high = forecast[days]['high']['fahrenheit']
        temp_low = forecast[days]['low']['fahrenheit']
        qpf_allday = forecast[days]['qpf_allday']['in']
        snow_allday = forecast[days]['snow_allday']['in']
    
        html = r'''
    <!DOCTYPE html>
    <html>
    <body>
        <center>
            <font size="1"><b>{}</b><br>
            {}°F / {}°F</font><br>
            <img src="img/{}">
        </center>
        <div align="left"><font size="1">
        <b>Conditions:</b> {}<br>
        <b>Percipitation:</b> {} in<br>
        <b>Snow Fall:</b> {} in
        </div></font>
    </body>
    </html>
        '''.format(weekday, temp_high, temp_low, condition_icon, condition,
                   qpf_allday, snow_allday)
        return html
    
    
    class Main(QWidget):
        def __init__(self):
            super(Main, self).__init__()
            self.ui = Ui_main()
            self.window = QWidget()
            self.ui.setupUi(self)
            base_url = 'http://api.wunderground.com/api/'
            conf = cp.ConfigParser()
            conf.read('settings.conf')
            api_key = conf['SETTINGS']['API_KEY']
            state = conf['SETTINGS']['STATE']
            city = conf['SETTINGS']['CITY']
            self.forecast_url = '{}{}/forecast10day/q/{}/{}.json'.format(base_url,
                                                                    api_key, state,
                                                                    city)
            self.current_url = '{}{}/conditions/q/{}/{}.json'.format(base_url, api_key,
                                                                state, city)
            #self.setWindowFlags(QtCore.Qt.Tool) # don't show in task manager
            test_connection(self.forecast_url, self.current_url)
            self.ui.weather_box0.insertHtml(display_current(self.current_url))
            self.ui.weather_box1.insertHtml(display_forecast(self.forecast_url, 0))
            self.ui.weather_box2.insertHtml(display_forecast(self.forecast_url, 1))
            self.ui.weather_box3.insertHtml(display_forecast(self.forecast_url, 2))
    
            self.ui.weather_box0.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
            self.ui.weather_box1.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
            self.ui.weather_box2.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
            self.ui.weather_box3.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
    
            self.current_timer = QtCore.QTimer()
            self.current_timer.start(900000)
            self.current_timer.timeout.connect(self.refresh_current)
    
            self.forecast_timer = QtCore.QTimer()
            self.forecast_timer.start(3600000)
            self.forecast_timer.timeout.connect(self.refresh_forecast)
    
        def refresh_current(self):
            self.ui.weather_box0.clear()
            self.ui.weather_box0.insertHtml(display_current(self.current_url))
    
        def refresh_forecast(self):
            self.ui.weather_box1.clear()
            self.ui.weather_box2.clear()
            self.ui.weather_box3.clear()
            self.ui.weather_box1.insertHtml(display_forecast(self.forecast_url, 0))
            self.ui.weather_box2.insertHtml(display_forecast(self.forecast_url, 1))
            self.ui.weather_box3.insertHtml(display_forecast(self.forecast_url, 2))
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        main = Main()
        main.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
