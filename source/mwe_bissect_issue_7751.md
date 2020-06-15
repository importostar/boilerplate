---
title: mwe_bissect_issue_7751
date: 2020-05-07
---
Example Python program mwe_bissect_issue_7751.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.path import Path
* from matplotlib.spines import Spine
* from matplotlib.projections.polar import PolarAxes
* from matplotlib.projections import register_projection

## Classes

* class RadarAxes(PolarAxes):

## Methods

* def radar_factory(num_vars, frame='circle'):
* def draw_poly_patch(self):
* def draw_circle_patch(self):
* def fill(self, *args, **kwargs):
* def plot(self, *args, **kwargs):
* def _close_line(self, line):
* def set_varlabels(self, labels):
* def _gen_axes_patch(self):
* def _gen_axes_spines(self):
* def unit_poly_verts(theta):

## Code

Python example

    """
    MWE to bissect issue #7751
    
    ======================================
    Radar chart (aka spider or star chart)
    ======================================
    
    This example creates a radar chart, also known as a spider or star chart [1]_.
    
    Although this example allows a frame of either 'circle' or 'polygon', polygon
    frames don't have proper gridlines (the lines are circles instead of polygons).
    It's possible to get a polygon grid by setting GRIDLINE_INTERPOLATION_STEPS in
    matplotlib.axis to the desired number of vertices, but the orientation of the
    polygon is not aligned with the radial axes.
    
    .. [1] http://en.wikipedia.org/wiki/Radar_chart
    """
    import numpy as np
    
    import matplotlib.pyplot as plt
    from matplotlib.path import Path
    from matplotlib.spines import Spine
    from matplotlib.projections.polar import PolarAxes
    from matplotlib.projections import register_projection
    
    
    def radar_factory(num_vars, frame='circle'):
        """Create a radar chart with `num_vars` axes.
    
        This function creates a RadarAxes projection and registers it.
    
        Parameters
        ----------
        num_vars : int
            Number of variables for radar chart.
        frame : {'circle' | 'polygon'}
            Shape of frame surrounding axes.
    
        """
        # calculate evenly-spaced axis angles
        theta = np.linspace(0, 2*np.pi, num_vars, endpoint=False)
        # rotate theta such that the first axis is at the top
        theta += np.pi/2
    
        def draw_poly_patch(self):
            verts = unit_poly_verts(theta)
            return plt.Polygon(verts, closed=True, edgecolor='k')
    
        def draw_circle_patch(self):
            # unit circle centered on (0.5, 0.5)
            return plt.Circle((0.5, 0.5), 0.5)
    
        patch_dict = {'polygon': draw_poly_patch, 'circle': draw_circle_patch}
        if frame not in patch_dict:
            raise ValueError('unknown value for `frame`: %s' % frame)
    
        class RadarAxes(PolarAxes):
    
            name = 'radar'
            # use 1 line segment to connect specified points
            #RESOLUTION = 1
            # define draw_frame method
            draw_patch = patch_dict[frame]
    
            def fill(self, *args, **kwargs):
                """Override fill so that line is closed by default"""
                closed = kwargs.pop('closed', True)
                return super(RadarAxes, self).fill(closed=closed, *args, **kwargs)
    
            def plot(self, *args, **kwargs):
                """Override plot so that line is closed by default"""
                lines = super(RadarAxes, self).plot(*args, **kwargs)
                for line in lines:
                    self._close_line(line)
    
            def _close_line(self, line):
                x, y = line.get_data()
                # FIXME: markers at x[0], y[0] get doubled-up
                if x[0] != x[-1]:
                    x = np.concatenate((x, [x[0]]))
                    y = np.concatenate((y, [y[0]]))
                    line.set_data(x, y)
    
            def set_varlabels(self, labels):
                self.set_thetagrids(np.degrees(theta), labels)
    
            def _gen_axes_patch(self):
                return self.draw_patch()
    
            def _gen_axes_spines(self):
                if frame == 'circle':
                    return PolarAxes._gen_axes_spines(self)
                # The following is a hack to get the spines (i.e. the axes frame)
                # to draw correctly for a polygon frame.
    
                # spine_type must be 'left', 'right', 'top', 'bottom', or `circle`.
                spine_type = 'circle'
                verts = unit_poly_verts(theta)
                # close off polygon by repeating first vertex
                verts.append(verts[0])
                path = Path(verts)
    
                spine = Spine(self, spine_type, path)
                spine.set_transform(self.transAxes)
                return {'polar': spine}
    
        register_projection(RadarAxes)
        return theta
    
    
    def unit_poly_verts(theta):
        """Return vertices of polygon for subplot axes.
    
        This polygon is circumscribed by a unit circle centered at (0.5, 0.5)
        """
        x0, y0, r = [0.5] * 3
        verts = [(r*np.cos(t) + x0, r*np.sin(t) + y0) for t in theta]
        return verts
    
    
    if __name__ == '__main__':
        N = 9
        theta = radar_factory(N, frame='polygon')
    
        # Why do I need to do that?
        eps = 0.15  # Add > 0 epsilon to data, to avoid artifacts in log scale
    
        data = ('Basecase', np.array([
                [0.88, 0.01, 0.03, 0.03, 0.00, 0.06, 0.01, 0.00, 0.00],
                [0.07, 0.95, 0.04, 0.05, 0.00, 0.02, 0.01, 0.00, 0.00],
                [0.01, 0.02, 0.85, 0.19, 0.05, 0.10, 0.00, 0.00, 0.00],
                [0.02, 0.01, 0.07, 0.01, 0.21, 0.12, 0.98, 0.00, 0.00],
                [0.01, 0.01, 0.02, 0.71, 0.74, 0.70, 0.00, 0.00, 0.00]]) + eps)
        spoke_labels = ['Sulfate', 'Nitrate', 'EC', 'OC1', 'OC2', 'OC3', 'OP',
                        'CO', 'O3']
    
        fig, ax = plt.subplots(figsize=(9, 9), subplot_kw=dict(projection='radar'))
    
        title, case_data = data
    
        ax.set_rscale('log')  # WiP: issue #7751
    
        for d, color in zip(case_data, ['C%d' % i for i in range(len(case_data))]):
            ax.plot(theta, d, color=color)
            ax.fill(theta, d, facecolor=color, alpha=0.25)
    
        ax.set_varlabels(spoke_labels)
    
        plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
