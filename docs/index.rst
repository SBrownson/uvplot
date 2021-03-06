.. uvplot documentation master file, created by
   sphinx-quickstart on Wed May 24 13:32:58 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


=========
|uvplot|
=========
A simple package to make nice plots of deprojected interferometric visibilities, often called **uvplots**.
It can be installed inside the `NRAO CASA package <https://casa.nrao.edu/>`_ (see instructions below) and has functionalities to export visibilities from the MS Table format to ASCII.

The current version implements the basic plotting functionality.

Features on the road map:
    - better handling of multiple spectral windows during visibilities export;
    - new functionality to import visibilities from ASCII to MS Table.

If you are interested, have feature requests, or encounter issues, consider creating an `Issue <https://github.com/mtazzari/uvplot/issues>`_ or writing me an `email  <marco.tazzari@gmail.com>`_. I am happy to have your feedback!


Attribution
-----------
If you use **uvplot** for your publication, please cite the `Zenodo reference <https://zenodo.org/badge/latestdoi/105298533>`_ ::

    @misc{uvplot_mtazzari,
      author       = {Marco Tazzari},
      title        = {mtazzari/uvplot: v0.1.1},
      month        = oct,
      year         = 2017,
      doi          = {10.5281/zenodo.1003113},
      url          = {https://doi.org/10.5281/zenodo.1003113}
    }


License
-------
**uvplot** is free software licensed under the LGPLv3 License. For more details see the LICENSE.
© Copyright 2018 Marco Tazzari.


Changelog
---------
- **v0.2.2**: a new export visibilities option in UVTable.plot(), automatically mask empty uv-bins, bugfixes.
- **v0.2.0**: a new `export_uvtable` function to export visibilities from an MS to an ASCII table.


Installation
------------

**uvplot** works on `Python` >=2.7 and >=3.6 and can be installed with:

.. code-block :: bash

    pip install uvplot

To make **uvplot** available in CASA, run from the shell:

.. code-block :: bash

    casa-pip install uvplot

where `casa-pip` is a tool that can be downloaded `here <https://github.com/radio-astro-tools/casa-python>`_ .

**uvplot** has been tested on CASA versions >= 4.7.0.

Example
-------
This is an example plot:

.. image:: images/uvplot.png
   :width: 60 %
   :alt: example uv plot
   :align: center

created with:

.. code-block:: py

    import numpy as np
    from uvplot import UVTable, arcsec

    wle = 0.88e-3         # Observing wavelength         [m]

    dRA = 0.3 * arcsec    # Delta Right Ascension offset [rad]
    dDec = 0.07 * arcsec  # Delta Declination     offset [rad]
    inc = np.radians(73.) # Inclination    [rad]
    PA = np.radians(59)   # Position Angle [rad]

    uvbin_size = 30e3     # uv-distance bin [wle]

    uv = UVTable(filename='uvtable.txt', wle=wle)
    uv.apply_phase(dRA, dDec)
    uv.deproject(inc, PA)

    uv_mod = UVTable(filename='uvtable_mod.txt', wle=wle)
    uv_mod.apply_phase(dRA=dRA, dDec=dDec)
    uv_mod.deproject(inc=inc, PA=PA)

    axes = uv.plot(label='Data', uvbin_size=uvbin_size)
    uv_mod.plot(label='Model', uvbin_size=uvbin_size, axes=axes, yerr=False, linestyle='-', color='r')

    axes[0].figure.savefig("uvplot.png")


© Copyright 2018 Marco Tazzari.

..    Contents
    --------
    .. toctree::
        :maxdepth: 2
    index
    Indices
    -------
    * :ref:`genindex`
    * :ref:`search`

