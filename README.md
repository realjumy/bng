# bng

Python functions to convert `osgb36` (EPSG:27700) coordinates to/from 4, 6, 8, or 10 figure grid references

This script was originally published on of the [Easily change coordinate projection systems in Python with pyproj](http://all-geo.org/volcan01010/2012/11/change-coordinates-with-pyproj/) blog post.
See blog post for more information and for details on converting other coordinate systems to `osbg36`.

# Instructions

The function converts between a bng grid reference as a string, and a tuple of OSGB36 (x,y) coordinates. When converting to bng coordinates, there is an opportunity to specify how many figures to use.

bng coordinates can be converted to osbg36 (EPSG:27700) coordinates as follows:

```python
>>> import bng # import the bng module
>>> bng.to_osgb36('NT2755072950')
(327550, 672950)
```

Combined with `pyproj` (see [blog post](http://all-geo.org/volcan01010/2012/11/change-coordinates-with-pyproj/)), this can be converted to GPS coordinates.
```python
>>> x, y = bng.to_osgb36('NT2755072950')
>>> pyproj.transform(osgb36, wgs84, x, y)
(-3.1615548588213667, 55.944109545140932)
```

Use Python’s zip function handle multiple values:
```python
>>> gridrefs = ['HU431392', 'SJ637560', 'TV374354']
>>> xy = bng.to_osgb36(gridrefs)
>>> x, y = zip(*xy)
>>> x
(443100, 363700, 537400)
>>> y
(1139200, 356000, 35400)
```

You can convert OSGB36 coordinates to bng coordinates like this:
```python
>>> bng.from_osgb36((327550, 672950))
'NT276730'
```

Again, use the zip function for multiple values. You can also specify the number of figures:
```python
>>> x = [443143, 363723, 537395]
>>> y = [1139158, 356004, 35394]
>>> xy = zip(x, y)
>>> bng.from_osgb36(xy, nDigits=4)
['HU4339', 'SJ6456', 'TV3735']
```

# For Developers

Install dependencies:

```bash
pip install -r requirements.txt
```

Run tests:

```bash
pytest -vs test_bng.py
```

# License
```
############################################################################
#
#  COPYRIGHT:  (C) 2012 John A Stevenson / @volcan01010
#           Magnus Hagdorn
#  WEBSITE: http://all-geo.org/volcan01010
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 3 of the License, or
#  (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  http://www.gnu.org/licenses/gpl-3.0.html
#
#############################################################################
```