# svg-path-to-polygons
Node package that converts path commands for an SVG path to polygonal points.

## Features

* Sparsely represents linear portions of the path by the minimal number of points.
* Does not skip any imporant features.
* Uses adaptive subsampling for curves to represent them exactly in the fewest number of points, with an arbitrary tolerance.


## Installation

`npm install svg-path-to-polygons`


## Usage
```js
const { pathDataToPolys } = require('../svg-path-to-polygons.js');
let pathData = 'M5,15 c5.5,0 10-4.5 10,-10 h10';
let points = pathDataToPolys(pathData, {tolerance:1, decimals:1});
console.log(points);
/*******************************************************************
[
  [ [5,15],[7,14.8],[10.6,13.3],[13.3,10.6],[14.8,7],[15,5],[25,5] ]
]
********************************************************************/
```

Note that the output for every path is an array of polygons/polylines (even if there is only one), where each polygon/polyline is an array of points, and where each point is an array of two numbers.

Each polygon/polyline also includes a custom `closed` property that defines whether the SVG subpath was closed (i.e. ended with a `z` or `Z` command).

The optional `tolerance` option specifies how far (in SVG coordinates) the polygon path may deviate from ideal curves. If not supplied, it defaults to `1`.

The optional `decimals` option controls the precision of values produces for each point. Only non-negative values are currently supported. If unspecified, full precision is used for each number.


## TODO (aka Known Limitations)

* Need to support quadratic Bézier commands.
* Need to support arc commands.
* Subsample linear sections if they are within the `tolerance`.
* Support negative values for `decimals`.

## License, Contact, and Support

Copyright 2017 Gavin Kistner (!@phrogz.net)
MIT License. See `LICENSE` file for details.

Please file bugs and feature requests [on the GitHub page](https://github.com/Phrogz/svg-path-to-polygons/issues).