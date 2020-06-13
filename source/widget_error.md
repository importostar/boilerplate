---
title: widget_error
date: 2020-05-07
---
Example Python program widget_error.py

## Modules

* 516 from PIL import Image

## Methods

* 345 def send_event(self, event_type, **kwargs):
* 379 def set_cursor(self, cursor):
* 345 def send_event(self, event_type, **kwargs):

## Code

Python example

    ---------------------------------------------------------------------------
    AttributeError                            Traceback (most recent call last)
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backend_bases.py in _wait_cursor_for_draw_cm(self)
       2772             try:
    -> 2773                 self.set_cursor(cursors.WAIT)
       2774                 yield
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_webagg_core.py in set_cursor(self, cursor)
        380         if cursor != self.cursor:
    --> 381             self.canvas.send_event("cursor", cursor=cursor)
        382         self.cursor = cursor
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_webagg_core.py in send_event(self, event_type, **kwargs)
        345     def send_event(self, event_type, **kwargs):
    --> 346         self.manager._send_event(event_type, **kwargs)
        347 
    
    AttributeError: 'NoneType' object has no attribute '_send_event'
    
    During handling of the above exception, another exception occurred:
    
    AttributeError                            Traceback (most recent call last)
    ~\.conda\envs\py5\lib\site-packages\IPython\core\formatters.py in __call__(self, obj)
        339                 pass
        340             else:
    --> 341                 return printer(obj)
        342             # Finally look for special method names
        343             method = get_real_method(obj, self.print_method)
    
    ~\.conda\envs\py5\lib\site-packages\IPython\core\pylabtools.py in <lambda>(fig)
        246 
        247     if 'png' in formats:
    --> 248         png_formatter.for_type(Figure, lambda fig: print_figure(fig, 'png', **kwargs))
        249     if 'retina' in formats or 'png2x' in formats:
        250         png_formatter.for_type(Figure, lambda fig: retina_figure(fig, **kwargs))
    
    ~\.conda\envs\py5\lib\site-packages\IPython\core\pylabtools.py in print_figure(fig, fmt, bbox_inches, **kwargs)
        130         FigureCanvasBase(fig)
        131 
    --> 132     fig.canvas.print_figure(bytes_io, **kw)
        133     data = bytes_io.getvalue()
        134     if fmt == 'svg':
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backend_bases.py in print_figure(self, filename, dpi, facecolor, edgecolor, orientation, format, bbox_inches, **kwargs)
       2061             if bbox_inches:
       2062                 if bbox_inches == "tight":
    -> 2063                     renderer = _get_renderer(
       2064                         self.figure,
       2065                         functools.partial(
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backend_bases.py in _get_renderer(figure, print_method)
       1532     with cbook._setattr_cm(figure, draw=_draw):
       1533         try:
    -> 1534             print_method(io.BytesIO())
       1535         except Done as exc:
       1536             figure._cachedRenderer, = exc.args
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_agg.py in print_png(self, filename_or_obj, metadata, pil_kwargs, *args, **kwargs)
        512         }
        513 
    --> 514         FigureCanvasAgg.draw(self)
        515         if pil_kwargs is not None:
        516             from PIL import Image
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_agg.py in draw(self)
        388         self.renderer = self.get_renderer(cleared=True)
        389         # Acquire a lock on the shared font cache.
    --> 390         with RendererAgg.lock, \
        391              (self.toolbar._wait_cursor_for_draw_cm() if self.toolbar
        392               else nullcontext()):
    
    ~\.conda\envs\py5\lib\contextlib.py in __enter__(self)
        111         del self.args, self.kwds, self.func
        112         try:
    --> 113             return next(self.gen)
        114         except StopIteration:
        115             raise RuntimeError("generator didn't yield") from None
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backend_bases.py in _wait_cursor_for_draw_cm(self)
       2774                 yield
       2775             finally:
    -> 2776                 self.set_cursor(self._lastCursor)
       2777         else:
       2778             yield
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_webagg_core.py in set_cursor(self, cursor)
        379     def set_cursor(self, cursor):
        380         if cursor != self.cursor:
    --> 381             self.canvas.send_event("cursor", cursor=cursor)
        382         self.cursor = cursor
        383 
    
    ~\.conda\envs\py5\lib\site-packages\matplotlib\backends\backend_webagg_core.py in send_event(self, event_type, **kwargs)
        344 
        345     def send_event(self, event_type, **kwargs):
    --> 346         self.manager._send_event(event_type, **kwargs)
        347 
        348 
    
    AttributeError: 'NoneType' object has no attribute '_send_event'

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
