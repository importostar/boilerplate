---
title: mpl.specgram
date: 2020-05-07
---
Example Python program mpl.specgram.py


## Methods

* def specgram(self, x, NFFT=None, Fs=None, Fc=None, detrend=None,

## Code

Python example

      @docstring.dedent_interpd
        def specgram(self, x, NFFT=None, Fs=None, Fc=None, detrend=None,
                     window=None, noverlap=None,
                     cmap=None, xextent=None, pad_to=None, sides=None,
                     scale_by_freq=None, mode=None, scale=None,
                     vmin=None, vmax=None, **kwargs):
            """
            Plot a spectrogram.
            """
    
            # selfとはaxexオブジェクトの事
    
            # axesをクリア
            if not self._hold:
                self.cla()
    
            # Fcが未入力の場合は0(軸目盛に使う)
            if Fc is None:
                Fc = 0
    
            # 複素数を扱うかの保障
            if mode == 'complex':
                raise ValueError('Cannot plot a complex specgram')
    
            # スケールの設定
            if scale is None or scale == 'default':
                if mode in ['angle', 'phase']:
                    scale = 'linear'
                else:
                    scale = 'dB'
            elif mode in ['angle', 'phase'] and scale == 'dB':
                raise ValueError('Cannot use dB scale with angle or phase mode')
    
            # stft解析
            spec, freqs, t = mlab.specgram(x=x, NFFT=NFFT, Fs=Fs,
                                           detrend=detrend, window=window,
                                           noverlap=noverlap, pad_to=pad_to,
                                           sides=sides,
                                           scale_by_freq=scale_by_freq,
                                           mode=mode)
            # スケールにより、解析結果を処理
            if scale == 'linear':
                Z = spec
            elif scale == 'dB':
                if mode is None or mode == 'default' or mode == 'psd':
                    Z = 10. * np.log10(spec)
                else:
                    Z = 20. * np.log10(spec)
            else:
                raise ValueError('Unknown scale %s', scale)
    
            # imshow()で表示するために、行列を反転
            Z = np.flipud(Z)
    
            # 目盛の最小値、最大値を設定
            if xextent is None:
                xextent = 0, np.amax(t)
            xmin, xmax = xextent
            freqs += Fc
            extent = xmin, xmax, freqs[0], freqs[-1]
    
            # imshowをプロット
            im = self.imshow(Z, cmap, extent=extent, vmin=vmin, vmax=vmax,
                             **kwargs)
            # アスペクト比をグラフサイズに合わせる
            self.axis('auto')
    
            return spec, freqs, t, im

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
