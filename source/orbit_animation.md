---
title: orbit_animation
date: 2020-05-07
---
Example Python program orbit_animation.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.widgets as mwidgets
* from datetime import datetime, timedelta
* import numpy as np
* import astropy.units as u
* import astropy.constants as const
* from astropy.visualization import quantity_support
* import matplotlib.gridspec as gridspec
* import matplotlib.ticker as mticker
* from matplotlib.animation import FFMpegWriter
* import heliopy.spice as spice
* import heliopy.data.spice as spicedata
* import spiceypy

## Classes

* class Body:

## Methods

* def dist_elev_azimuth(x, y, z):
* def parker_spiral_phi(phi_0):
* def plot_timeseries(bodies, times, coords):
* def setup_animation_axes(ax):
* def run_animation(bodies, times, coords, fig, axs, ax, vlines, fname):
* def date2ndays(d):
* def ndays2date(n):
* def update(dtime):
* def animate(bodies, times, coords, fname):
* def __init__(self, name, plot_tseries, color, stime=None):
* def generate_trajectory(self, times, coords):
* def generate_times(start, end, delta):

## Code

Python example

    import matplotlib
    matplotlib.use('qt5agg')
    import matplotlib.pyplot as plt
    import matplotlib.widgets as mwidgets
    
    from datetime import datetime, timedelta
    import numpy as np
    import astropy.units as u
    import astropy.constants as const
    from astropy.visualization import quantity_support
    import matplotlib.gridspec as gridspec
    import matplotlib.ticker as mticker
    from matplotlib.animation import FFMpegWriter
    
    import heliopy.spice as spice
    import heliopy.data.spice as spicedata
    import spiceypy
    
    
    def dist_elev_azimuth(x, y, z):
        dist = np.sqrt(x**2 + y**2 + z**2)
        elev = np.rad2deg(np.arcsin(z / dist))
        az = np.rad2deg(np.arctan2(y, x))
        return dist, elev, az
    
    
    omega_sun = 405 * u.km * u.rad / u.s / const.au
    vsw = 500 * u.km / u.s
    spiral_rs_au = np.linspace(0, 2, 100) * const.au
    spiral_rs = (spiral_rs_au / const.au).value
    
    
    def parker_spiral_phi(phi_0):
        return phi_0 + omega_sun * spiral_rs_au / vsw
    
    
    def plot_timeseries(bodies, times, coords):
        quantity_support()
    
        gs = gridspec.GridSpec(7, 1)
        fig = plt.figure(figsize=(10, 10))
        ax1 = plt.subplot(gs[0, 0])
        ax2 = plt.subplot(gs[1, 0], sharex=ax1)
        ax3 = plt.subplot(gs[2, 0], sharex=ax1)
        ax_orbit = plt.subplot(gs[4:, 0])
        fig.subplots_adjust(hspace=0)
        axs = [ax1, ax2, ax3]
        for ax in axs[:-1]:
            ax.xaxis.set_visible(False)
    
        for body in bodies:
            traj = body.trajectory
            dist, elev, az = dist_elev_azimuth(traj.x, traj.y, traj.z)
            axs[0].plot(traj.times, traj.r, lw=1, color=body.color)
            axs[1].plot(traj.times, elev, lw=1, color=body.color)
            axs[2].scatter(traj.times, az, s=0.5, color=body.color)
    
        axs[0].set_ylim(0, 1.1)
        axs[0].set_ylabel('r (AU)')
    
        axs[1].set_ylabel('Elevation')
        axs[1].set_ylim(-16, 16)
        axs[1].axhline(0, color='k', lw=1, linestyle='--')
    
        axs[2].set_ylabel('Azimuth')
        for val in [-90, 0, 90]:
            axs[2].axhline(val, color='k', lw=1, linestyle='--')
        axs[2].set_ylim(-180, 180)
        axs[2].yaxis.set_major_locator(mticker.FixedLocator([-90, 0, 90]))
    
        vlines = []
        for a in axs:
            line = a.axvline(starttime, color='k', lw=1)
            vlines.append(line)
            a.set_xlim(times[0], times[-1])
    
        return fig, axs, ax_orbit, vlines
    
    
    def setup_animation_axes(ax):
        ax.scatter(0, 0, s=70, color='#feb24c', edgecolors='k', label='Sun')
        ax.set_xlim(-1.1, 1.1)
        ax.set_ylim(-1.1, 1.1)
        ax.set_xlabel('x (AU)')
        ax.set_ylabel('y (AU)')
        ax.set_aspect('equal', adjustable='box')
    
    
    def run_animation(bodies, times, coords, fig, axs, ax, vlines, fname):
        # Use this as a reference date
        base_date = datetime(1974, 1, 1)
    
        def date2ndays(d):
            # Return number of days since base_date
            return (d - base_date).total_seconds() / (60 * 60 * 24)
    
        def ndays2date(n):
            # Return date given number of days since base_date
            return base_date + timedelta(days=n)
    
        # Scatter initial positions
        scatter_kwargs = {'marker': 'o', 'ms': 10, 'mec': 'k', 'zorder': 1}
        circles = {}
        lines = {}
        spirals = []
    
        # List of all the artists
        artists = []
    
        # Create initial body artists
        for body in bodies:
            circle, = ax.plot([], [],
                              label=body.name,
                              color=body.color,
                              **scatter_kwargs)
            line, = ax.plot([], [], color=body.color, zorder=-1)
            circles[body] = circle
            lines[body] = line
            artists.append(circle)
            artists.append(line)
    
        # Create initial spiral artists
        spirals = []
        for phi_0 in np.linspace(0, 2 * np.pi, 5)[:-1] * u.rad:
            phi = parker_spiral_phi(phi_0)
            line, = ax.plot(spiral_rs * np.sin(phi),
                            spiral_rs * np.cos(phi),
                            color='black', lw=1, zorder=-2, alpha=0.5)
            spirals.append([line, phi_0])
            artists.append(line)
    
        ax.legend(loc='upper left', bbox_to_anchor=(1, 1))
        dt = times[1] - times[0]
    
        def update(dtime):
            print(dtime)
            for body in bodies:
                # Get index of datetime
                index = np.where(body.times == dtime)[0]
                if index.size == 0:
                    continue
                elif index.size == 1:
                    index = index[0]
                else:
                    raise RuntimeError('Index bigger than 1')
    
                index_current = index
                if coords == 'IAU_SUN':
                    rewind = 7
                else:
                    rewind = 14
                index_rewind = index - int(timedelta(days=rewind) / dt)
                if index_rewind < 0:
                    index_rewind = 0
    
                if index_current >= 0:
                    x = body.trajectory.x.value
                    y = body.trajectory.y.value
                    xdata = x[index_current]
                    ydata = y[index_current]
                    lines[body].set_xdata(x[index_rewind:index_current + 1])
                    lines[body].set_ydata(y[index_rewind:index_current + 1])
                    circles[body].set_xdata(xdata)
                    circles[body].set_ydata(ydata)
    
            if coords != 'IAU_SUN':
                delta_t = (dtime - times[0]).total_seconds() * u.s
                delta_phi_0 = omega_sun * delta_t
                for line, phi_0 in spirals:
                    phi = parker_spiral_phi(phi_0 - delta_phi_0)
                    line.set_xdata(spiral_rs * np.sin(phi))
                    line.set_ydata(spiral_rs * np.cos(phi))
    
            # Set date title
            ax.set_title(dtime.strftime('%d-%m-%Y'))
    
            # Change vlines
            for line in vlines:
                line.set_xdata(dtime)
    
            return artists
    
        # frames = range(len(times))
        moviewriter = FFMpegWriter(fps=24)
        with moviewriter.saving(fig, fname, dpi=100):
            for t in times:
                update(t)
                moviewriter.grab_frame()
    
    
    def animate(bodies, times, coords, fname):
        '''
        bodies : list of string
            List of bodies to add to animation.
        times : list of datetimes
            List of datetimes to generate positions for for each body.
        coords : str
            Coordinates
        '''
        tseries_kernels = [b for b in bodies if b.plot_tseries]
        fig, axs, ax_anim, vlines = plot_timeseries(tseries_kernels, times, coords)
        setup_animation_axes(ax_anim)
        run_animation(bodies, times, coords, fig, axs, ax_anim, vlines, fname)
    
    
    class Body:
        def __init__(self, name, plot_tseries, color, stime=None):
            self.name = name
            self.plot_tseries = plot_tseries
            self.color = color
            self.stime = stime
    
        def generate_trajectory(self, times, coords):
            traj = spice.Trajectory(self.name)
            if self.stime is None:
                gen_times = np.array(times)
            else:
                gen_times = np.array(times)
                gen_times = gen_times[gen_times > self.stime]
    
            traj.generate_positions(gen_times, 'Sun', coords)
            traj.change_units(u.au)
            self.times = gen_times
            self.trajectory = traj
    
    
    def generate_times(start, end, delta):
        times = []
        while start < end:
            times.append(start)
            start += delta
        return times
    
    
    if __name__ == '__main__':
        psp_kernels = spicedata.get_kernel('psp_pred')
        spice.furnish(psp_kernels)
    
        orbiter_kernel = spicedata.get_kernel('solo_2020')
        spice.furnish(orbiter_kernel)
    
        stereo_kernel = spicedata.get_kernel('stereo_a_pred')
        spice.furnish(stereo_kernel)
        coords = 'ECLIPJ2000'
    
        starttime = datetime(2018, 8, 13)
        endtime = datetime(2021, 6, 1)
        delta = timedelta(hours=12)
        times = generate_times(starttime, endtime, delta)
    
        spiceypy.spiceypy.boddef('PSP', -96)
        spiceypy.spiceypy.boddef('STEREO-A', -234)
        bodies = [Body('Solar Orbiter', True, 'C3', stime=datetime(2020, 2, 10)),
                  Body('PSP', True, 'C0'),
                  Body('STEREO-A', False, 'C4'),
                  Body('Earth', False, 'C2'),
                  ]
    
        for body in bodies:
            body.generate_trajectory(times, coords)
    
        fname = f'Movies/website/{coords}.mp4'
        animate(bodies, times, coords, fname)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
