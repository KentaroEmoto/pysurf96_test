# PySurf96

![Python3](https://img.shields.io/badge/python-3.x-brightgreen.svg)
<a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>

_Modelling Surface Wave Dispersion Curves_

This is a slim wrapper around the program `surf96` from _Computer programs in seismology_ by R. Hermann (<http://www.eas.slu.edu/eqc/eqccps.html>) for forward modelling of Rayleigh and Love wave dispersion curves.

In this realisation the Fortran77 code is wrapped by `f2py`, which makes the forward computation approximately **8x faster** compared over calling a Python subprocess.

More useful software for seismology at <https://pyrocko.org>.

## Installation

This package is for Python 3.

Prerequisits is a Fortran77 compiler, like GNU GCC.

```
pip3 install .
```

Or through pip:

```
pip install git+https://github.com/miili/pysurf96
```

## Example

```python
import numpy as np
from pysurf96 import surf96

# Define the velocity model in km and km/s
thickness = np.array([5.0, 23.0, 8.0, 0])
vs = np.array([2, 3.6, 3.8, 3.3])
vp = vs * 1.73
rho = vp * 0.32 + 0.77

# Periods we are interested in
periods = np.linspace(1.0, 20.0, 20)

velocities = surf96(
    thickness,
    vp,
    vs,
    rho,
    periods,
    wave="love",
    mode=1,
    velocity="group",
    flat_earth=True,

```

## Citations and Acknowledgments

> Herrmann, R. B. (2013) Computer programs in seismology: An evolving tool for instruction and research, Seism. Res. Lettr. 84, 1081-1088, doi:10.1785/0220110096

Thanks to Hongjian Fang for creating the Fortran subroutine (<https://github.com/caiweicaiwei/SurfTomo>)
