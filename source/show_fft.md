---
title: show_fft
date: 2020-05-07
---
Example Python program show_fft.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* import wx
* import pyaudio
* import wave
* from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
* from matplotlib.figure import Figure
* import numpy as np

## Classes

* class WavePanel(wx.Panel):

## Methods

* def __init__(self, parent):
* def init_graph(self):
* def update_graph(self, event):
* def draw(self, event=None):
* def fft_plot(self, data):
* def check_audio_devices():
* def main():

## Code

Python example

    # -*- coding: utf-8 -*-
    
    """
    Display fft data.
    
    Environment:
    matplotlib==2.0.2
    numpy==1.13.0
    PyAudio==0.2.11
    wxPython==4.0.0a3
    """
    
    
    import matplotlib
    matplotlib.interactive(True)
    matplotlib.use('WXAgg')
    
    import wx
    
    import pyaudio
    import wave
    
    from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
    from matplotlib.figure import Figure
    import numpy as np
    
    
    CHUNK = 1024 * 4
    RATE = 44100
    
    class WavePanel(wx.Panel):
        """
        Display fft data.
        """
        
        def __init__(self, parent):
            self.parent = parent
            wx.Panel.__init__(self, parent)
            
            self.lastplot = None
    
            # matplotlib figure
            self.figure = Figure(None)
            self.figure.set_facecolor((0.9, 0.9, 1.))
            self.subplot = self.figure.add_subplot(111)
            # canvas
            self.canvas = FigureCanvasWxAgg(self, -1, self.figure)
            self.canvas.SetBackgroundColour(wx.Colour(100,255,255))
    
            # Layout using BoxSizer
            sizer = wx.BoxSizer(wx.VERTICAL)
            sizer.Add(self.canvas, 1, wx.EXPAND)
            self.SetSizer(sizer)
            
            self.init_graph()
            
            # pyaudio
            # self.wavefile = wave.open('data/musicbox.wav', 'rb')
            self.pyaudio = pyaudio.PyAudio()
            self.stream = self.pyaudio.open(format=pyaudio.paInt16,
                            channels=2,
                            rate=RATE,
                            input_device_index=2,  # speaker(soundflower2ch) id
                            frames_per_buffer=CHUNK,
                            input=True,
                            output=True)
            
            # Redraw graph with timer
            self.timer = wx.Timer(self, 1)
            self.Bind(wx.EVT_TIMER, self.update_graph, self.timer)
            self.timer.Start(15)
        
        def init_graph(self):
            """
            Set up graph except for plotting.
            """
            self.subplot.set_title('sample (fft)')
            self.subplot.set_xlabel('freq')
            self.subplot.set_ylabel('y')
            self.subplot.set_xscale('log')
            # self.subplot.set_yscale('log')  # If use amplitude spectrum
    
        def update_graph(self, event):
            """
            Redraw graph.
            """
            self.draw(event)
    
        def draw(self, event=None):
            """
            Draw plotting data.
            """
            # Read audio data
            # data = self.wavefile.readframes(CHUNK)
            # if data != b'':
            if self.stream.is_active():
                data = self.stream.read(CHUNK, exception_on_overflow=False)
                if self.lastplot and self.lastplot[0]:
                    self.lastplot[0].remove()
                # self.stream.write(data)  # output audio data
                x, y = self.fft_plot(data)
                self.lastplot = self.subplot.plot(x, y, 'b')  # 3rd param is line color
            else:
                # release resources
                self.stream.stop_stream()
                self.stream.close()
                self.pyaudio.terminate()
                self.timer.Stop()
    
            self.canvas.draw()
    
        def fft_plot(self, data):
            """
            Create plotting data from data param.
            """
            data1 = np.frombuffer(data, dtype='int16') / 32768.0  # Normalize
            data = np.hamming(len(data1)) * data1  # hamming window
            fft_data = np.fft.fft(data)
            fft_data = np.abs(fft_data)
            # fft_data = 20 * np.log10(fft_data)  # amplitude spectrum(db)
            x = np.fft.fftfreq(len(fft_data), d=0.5 / RATE)
            x = np.abs(x)
            return x, fft_data
    
    
    def check_audio_devices():
        """
        Display valid devices on PC. Use the device id for "input_device_index"
        on "pyaudio.open()"
        """
        p = pyaudio.PyAudio()
        info = p.get_host_api_info_by_index(0)
        numdevices = info.get('deviceCount')
        for i in range(0, numdevices):
                if (p.get_device_info_by_host_api_device_index(0, i).get('maxInputChannels')) > 0:
                    print("Input Device id ", i, " - ", p.get_device_info_by_host_api_device_index(0, i).get('name'))
    
    def main():
        app = wx.App()
        frame = wx.Frame(None, size=(700,500))
        panel = WavePanel(frame)
        frame.Show()
        app.MainLoop()
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
