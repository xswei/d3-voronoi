# d3-voronoi

这个模块实现了用来计算一组二维点 [Voronoi diagram(泰森多边形)](https://en.wikipedia.org/wiki/Voronoi_diagram) 或 [Delaunay triangulation(德劳内三角剖分)](https://en.wikipedia.org/wiki/Delaunay_triangulation) 的 [Steven J. Fortune’s algorithm](https://en.wikipedia.org/wiki/Fortune's_algorithm) 算法。这个模块的实现大多是基于 [Raymond Hill](http://www.raymondhill.net/voronoi/rhill-voronoi.html) 的工作。

泰森多边形不仅仅在视觉上具有吸引力，在交互方面也非常实用，比如在散点图中增加点的目标面积。参考 [“Strikeouts on the Rise”](http://www.nytimes.com/interactive/2013/03/29/sports/baseball/Strikeouts-Are-Still-Soaring.html) 和 [multi-line chart](http://bl.ocks.org/mbostock/8033015)。也可以参考 Tovi Grossman’s 的关于关联技术的 [bubble cursors](http://www.tovigrossman.com/BubbleCursor) 论文。泰森多边形也可以用来自动标记定位，德劳内网格在计算相邻域或视觉元素分组方面很有用。

<a href="http://bl.ocks.org/mbostock/6675193"><img src="http://bl.ocks.org/mbostock/raw/6675193/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/4060366"><img src="http://bl.ocks.org/mbostock/raw/4060366/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/4341156"><img src="http://bl.ocks.org/mbostock/raw/4341156/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/4360892"><img src="http://bl.ocks.org/mbostock/raw/4360892/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/7608400"><img src="http://bl.ocks.org/mbostock/raw/7608400/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/4636377"><img src="http://bl.ocks.org/mbostock/raw/4636377/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/1073373"><img src="http://bl.ocks.org/mbostock/raw/1073373/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/8033015"><img src="http://bl.ocks.org/mbostock/raw/8033015/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/c6966db1fcb0ed2988da"><img src="http://bl.ocks.org/mbostock/raw/c6966db1fcb0ed2988da/thumbnail.png" width="202"></a>
<a href="http://bl.ocks.org/mbostock/ec10387f24c1fad2acac3bc11eb218a5"><img src="http://bl.ocks.org/mbostock/raw/ec10387f24c1fad2acac3bc11eb218a5/thumbnail.png" width="202"></a>

## Installing

If you use NPM, `npm install d3-voronoi`. Otherwise, download the [latest release](https://github.com/d3/d3-voronoi/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-voronoi.v1.min.js) or as part of [D3 4.0](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

```html
<script src="https://d3js.org/d3-voronoi.v1.min.js"></script>
<script>

var voronoi = d3.voronoi();

</script>
```

[Try d3-voronoi in your browser.](https://tonicdev.com/npm/d3-voronoi)

## API Reference

<a name="voronoi" href="#voronoi">#</a> d3.<b>voronoi</b>() [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js "Source")

Creates a new Voronoi layout with default [*x*-](#voronoi_x) and [*y*-](#voronoi_y) accessors and a null [extent](#voronoi_extent).

<a name="_voronoi" href="#_voronoi">#</a> <i>voronoi</i>(<i>data</i>) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L10 "Source")

Computes the [Voronoi diagram](#voronoi-diagrams) for the specified *data* points.

<a name="voronoi_x" href="#voronoi_x">#</a> <i>voronoi</i>.<b>x</b>([<i>x</i>]) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L31 "Source")

If *x* is specified, sets the *x*-coordinate accessor. If *x* is not specified, returns the current *x*-coordinate accessor, which defaults to:

```js
function x(d) {
  return d[0];
}
```

<a name="voronoi_y" href="#voronoi_y">#</a> <i>voronoi</i>.<b>y</b>([<i>y</i>]) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L35 "Source")

If *y* is specified, sets the *y*-coordinate accessor. If *y* is not specified, returns the current *y*-coordinate accessor, which defaults to:

```js
function y(d) {
  return d[1];
}
```

<a name="voronoi_extent" href="#voronoi_extent">#</a> <i>voronoi</i>.<b>extent</b>([<i>extent</i>]) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L39 "Source")

If *extent* is specified, sets the clip extent of the Voronoi layout to the specified bounds and returns the layout. The *extent* bounds are specified as an array \[\[<i>x0</i>, <i>y0</i>\], \[<i>x1</i>, <i>y1</i>\]\], where <i>x0</i> is the left side of the extent, <i>y0</i> is the top, <i>x1</i> is the right and <i>y1</i> is the bottom. If *extent* is not specified, returns the current clip extent which defaults to null. A clip extent is required when using [*voronoi*.polygons](#voronoi_polygons).

<a name="voronoi_size" href="#voronoi_size">#</a> <i>voronoi</i>.<b>size</b>([<i>size</i>]) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L43 "Source")

An alias for [*voronoi*.extent](#voronoi_extent) where the minimum *x* and *y* of the extent are ⟨0,0⟩. Equivalent to:

```js
voronoi.extent([[0, 0], size]);
```

<a name="voronoi_polygons" href="#voronoi_polygons">#</a> <i>voronoi</i>.<b>polygons</b>(<i>data</i>) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L19 "Source")

Returns a sparse array of polygons, one for each unique input point in the specified *data* points, corresponding to the cells in the computed Voronoi diagram. Equivalent to:

```js
voronoi(data).polygons();
```

See [*diagram*.polygons](#diagram_polygons) for more detail. Note: an [extent](#voronoi_extent) is required.

<a name="voronoi_triangles" href="#voronoi_triangles">#</a> <i>voronoi</i>.<b>triangles</b>(<i>data</i>) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L27 "Source")

Returns the Delaunay triangulation of the specified *data* array as an array of triangles. Each triangle is a three-element array of elements from *data*. Equivalent to:

```js
voronoi(data).triangles();
```

See [*diagram*.triangles](#diagram_triangles) for more detail.

<a name="voronoi_links" href="#voronoi_links">#</a> <i>voronoi</i>.<b>links</b>(<i>data</i>) [<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L23 "Source")

Returns the Delaunay triangulation of the specified *data* array as an array of links. Each link has `source` and `target` attributes referring to elements in *data*. Equivalent to:

```js
voronoi(data).links();
```

See [*diagram*.links](#diagram_links) for more detail.

### Voronoi Diagrams

<a name="diagram" href="#diagram">#</a> <i>diagram</i> [<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js "Source")

The computed Voronoi diagram returned by [*voronoi*](#_voronoi) has the following properties:

* `edges` - an array of [edges](#diagram_edge).
* `cells` - a sparse array of [cells](#diagram_cell), one for each unique input point.

For each set of coincident input points, one of the points is chosen arbitrarily and assigned the associated cell; the other coincident input points’ entries are missing from the returned sparse array.

<a name="diagram_polygons" href="#diagram_polygons">#</a> <i>diagram</i>.<b>polygons</b>() [<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L72 "Source")

Returns a sparse array of polygons clipped to the [*extent*](#voronoi_extent), one for each cell (each unique input point) in the diagram. Each polygon is represented as an array of points \[*x*, *y*\] where *x* and *y* are the point coordinates, and a `data` field that refers to the corresponding element in *data*. Polygons are open: they do not contain a closing point that duplicates the first point; a triangle, for example, is an array of three points. Polygons are also counterclockwise, assuming the origin ⟨0,0⟩ is in the top-left corner.

For each set of coincident input points, one of the points is chosen arbitrarily and assigned the associated polygon; the other coincident input points’ entries are missing from the returned sparse array.

<a name="diagram_triangles" href="#diagram_triangles">#</a> <i>diagram</i>.<b>triangles</b>() [<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L82 "Source")

Returns the Delaunay triangulation of the specified *data* array as an array of triangles. Each triangle is a three-element array of elements from *data*. Since the triangulation is computed as the dual of the Voronoi diagram, and the Voronoi diagram is clipped by the [extent](#voronoi_extent), a subset of the Delaunay triangulation is returned.

<a name="diagram_links" href="#diagram_links">#</a> <i>diagram</i>.<b>links</b>() [<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L108 "Source")

Returns the Delaunay triangulation of the specified *data* array as an array of links, one for each edge in the mesh. Each link has the following attributes:

* `source` - the source node, an element in *data*.
* `target` - the target node, an element in *data*.

Since the triangulation is computed as the dual of the Voronoi diagram, and the Voronoi diagram is clipped by the [extent](#voronoi_extent), a subset of the Delaunay links is returned.

<a name="diagram_find" href="#diagram_find">#</a> <i>diagram</i>.<b>find</b>(<i>x</i>, <i>y</i>[, <i>radius</i>]) [<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L119 "Source")

Returns the nearest site to point \[*x*, *y*\]. If *radius* is specified, only sites within *radius* distance are considered.

See Philippe Rivière’s [bl.ocks.org/1b7ddbcd71454d685d1259781968aefc](http://bl.ocks.org/Fil/1b7ddbcd71454d685d1259781968aefc) for an example.

<a name="cell" href="#cell">#</a> <i>cell</i>

Each cell in the diagram is an object with the following properties:

* `site` - the [site](#site) of the cell’s associated input point.
* `halfedges` - an array of indexes into [*diagram*.edges](#diagram) representing the cell’s polygon.

<a name="site" href="#site">#</a> <i>site</i>

Each site in the diagram is an array \[*x*, *y*\] with two additional properties:

* `index` - the site’s index, corresponding to the associated input point.
* `data` - the input data corresponding to this site.

<a name="edge" href="#edge">#</a> <i>edge</i>

Each edge in the diagram is an array \[\[*x0*, *y0*\], \[*x1*, *y1*\]\] with two additional properties:

* `left` - the [site](#site) on the left side of the edge.
* `right` - the [site](#site) on the right side of the edge; null for a clipped border edge.
