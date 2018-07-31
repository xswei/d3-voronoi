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

`NPM` 安装: `npm install d3-voronoi`. 此外还可以下载 [latest release](https://github.com/d3/d3-voronoi/releases/latest). 可以直接从 [d3js.org](https://d3js.org) 以 [standalone library](https://d3js.org/d3-voronoi.v1.min.js) 或作为 [D3 4.0](https://github.com/d3/d3) 的一部分载入. 支持 `AMD`, `CommonJS`, 以及基本的标签引入形式。如果使用标签引入则会暴露全局 `d3` 变量:

```html
<script src="https://d3js.org/d3-voronoi.v1.min.js"></script>
<script>

var voronoi = d3.voronoi();

</script>
```

[在浏览器中测试 `d3-voronoi`.](https://tonicdev.com/npm/d3-voronoi)

## API Reference

<a name="voronoi" href="#voronoi">#</a> d3.<b>voronoi</b>() [<源码>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js "Source")

使用默认的 [*x*-](#voronoi_x) 和 [*y*-](#voronoi_y) 访问器创建一个新的泰森多边形布局，并且 [extent](#voronoi_extent) 为 `null`.

<a name="_voronoi" href="#_voronoi">#</a> <i>voronoi</i>(<i>data</i>) [<源码>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L10 "Source")

根据指定的 *data* 点数组计算 [Voronoi diagram](#voronoi-diagrams).

<a name="voronoi_x" href="#voronoi_x">#</a> <i>voronoi</i>.<b>x</b>([<i>x</i>]) [<源码>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L31 "Source")

如果指定了 *x* 则将 *x* 坐标访问器设置为指定的参数。如果没有指定 *x* 则返回当前的 *x* 坐标访问器，默认为:

```js
function x(d) {
  return d[0];
}
```

<a name="voronoi_y" href="#voronoi_y">#</a> <i>voronoi</i>.<b>y</b>([<i>y</i>]) [<源码>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L35 "Source")

如果指定了 *y* 则将 *y* 坐标访问器设置为指定的参数。如果没有指定 *y* 则返回当前的 *y* 坐标访问器，默认为:

```js
function y(d) {
  return d[1];
}
```

<a name="voronoi_extent" href="#voronoi_extent">#</a> <i>voronoi</i>.<b>extent</b>([<i>extent</i>]) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L39 "Source")

如果指定了 *extent* 则设置泰森多边形的裁剪范围为指定的范围并返回当前泰森多边形布局。*extent* 通过数组 \[\[<i>x0</i>, <i>y0</i>\], \[<i>x1</i>, <i>y1</i>\]\] 的形式指定，其中 <i>x0</i> 为左边界, <i>y0</i> 为上边界, <i>x1</i> 为右边界而 <i>y1</i> 为下边界。如果 *extent* 没有指定，则返回当前的裁剪范围，默认为 `null`。在使用 [*voronoi*.polygons](#voronoi_polygons) 时需要设置裁剪范围。

<a name="voronoi_size" href="#voronoi_size">#</a> <i>voronoi</i>.<b>size</b>([<i>size</i>]) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L43 "Source")

当裁剪范围最小 *x* 和 *y* 为 ⟨0,0⟩ 时相当于 [*voronoi*.extent](#voronoi_extent) 的别名。等价于:

```js
voronoi.extent([[0, 0], size]);
```

<a name="voronoi_polygons" href="#voronoi_polygons">#</a> <i>voronoi</i>.<b>polygons</b>(<i>data</i>) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L19 "Source")

返回一个稀疏的多边形数组，每个输入点对应一个多边形，相当于计算后的泰森多边形中的每一个多边形格子。等价于:

```js
voronoi(data).polygons();
```

参考 [*diagram*.polygons](#diagram_polygons) 获取更多信息. 注意: 需要设置 [extent](#voronoi_extent).

<a name="voronoi_triangles" href="#voronoi_triangles">#</a> <i>voronoi</i>.<b>triangles</b>(<i>data</i>) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L27 "Source")

根据指定的 *data* 返回德劳内三角剖分之后的三角形数组。每个三角形的三个顶点都来自 *data*。等价于:

```js
voronoi(data).triangles();
```

参考 [*diagram*.triangles](#diagram_triangles) 获取更多细节.

<a name="voronoi_links" href="#voronoi_links">#</a> <i>voronoi</i>.<b>links</b>(<i>data</i>) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/voronoi.js#L23 "Source")

返回对指定 *data* 的德劳内三角剖分的边数组，每个边包含 `source` 和 `target` 属性，并且都属于 *data* 中的某个元素。等价于:

```js
voronoi(data).links();
```

参考 [*diagram*.links](#diagram_links) 获取更多细节.

### Voronoi Diagrams

<a name="diagram" href="#diagram">#</a> <i>diagram</i> [<源码>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js "Source")

由 [*voronoi*](#_voronoi) 计算返回的泰森多边形包含以下属性:

* `edges` - [edges](#diagram_edge) 数组.
* `cells` - [cells](#diagram_cell) 稀疏数组, 每个元素对应一个唯一的输入点.

如果输入数据中存在多个完全一样的输入点，则其中一个会被与 `cell(单元)` 关联，而其他的相同的则被丢失，但不影响 `cells` 数组的长度(稀疏数组)。

<a name="diagram_polygons" href="#diagram_polygons">#</a> <i>diagram</i>.<b>polygons</b>() [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L72 "Source")

返回一个稀疏的并且根据 [*extent*](#voronoi_extent) 被裁剪的多边形数组，每个多边形都有一个对应的 `cell(单元)` (去重的稀疏单元)。每个多边形都由以个使用 \[*x*, *y*\] 组成的数组表示(二维数组)， 其中 *x* 和 *y* 表示多边形的定点。每个多边形二维数组包含一个 *data* 字段指向 *data* 中的对应元素。多边形是开放的: 不包含重复第一个的闭合点；例如，一个三角形是三个点的数组。多边形也是逆时针的，假设原点 ⟨0,0⟩ 在左上角。

对于输入数据中的重合点，其中一个点会被分配给多边形，而其他相同的点在返回的稀疏数组中丢失。

<a name="diagram_triangles" href="#diagram_triangles">#</a> <i>diagram</i>.<b>triangles</b>() [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L82 "Source")

根据指定的 *data* 返回德劳内三角剖分之后的三角形数组。每个三角形的三个定点都来自输入数据 *data*。由于三角剖分受 [extent](#voronoi_extent) 的影响，最后返回的是德劳内三角剖分的子集。

<a name="diagram_links" href="#diagram_links">#</a> <i>diagram</i>.<b>links</b>() [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L108 "Source")

返回对指定 *data* 德劳内三角剖分后的边数组，边对应网格中的每一条边。每个边包含以下两个属性:

* `source` - `source` 节点，*data* 中的某个元素.
* `target` - `target` 节点，*data* 中的某个元素.

受 [extent](#voronoi_extent) 的影响，最后返回的边数组是德劳内三角剖分后的边数组的子集。

<a name="diagram_find" href="#diagram_find">#</a> <i>diagram</i>.<b>find</b>(<i>x</i>, <i>y</i>[, <i>radius</i>]) [源码<>](https://github.com/d3/d3-voronoi/blob/master/src/Diagram.js#L119 "Source")

返回距离点 \[*x*, *y*\] 最近的点。如果指定了 *radius* 则仅仅在指定半径范围内查找。

参考 `Philippe Rivière` 的 [bl.ocks.org/1b7ddbcd71454d685d1259781968aefc](http://bl.ocks.org/Fil/1b7ddbcd71454d685d1259781968aefc) 查看例子。

<a name="cell" href="#cell">#</a> <i>cell</i>

每个单元都是包含以下两个属性的对象:

* `site` - 与单元格关联的输入数据中的 [site](#site).
* `halfedges` - 一组 [*diagram*.edges](#diagram) 的索引，表示单元格多边形的每条边.

<a name="site" href="#site">#</a> <i>site</i>

图中每个 `site` 都是一个 \[*x*, *y*\] 数组，并且包含以下两个属性:

* `index` - `site` 的索引，对应输入数据中相关数据的索引.
* `data` - 对应此 `site` 的输入数据.

<a name="edge" href="#edge">#</a> <i>edge</i>

每个边都被定义为 \[\[*x0*, *y0*\], \[*x1*, *y1*\]\]，并且包含以下两个属性:

* `left` - 边的左侧 [site](#site).
* `right` - 边的右侧 [site](#site); 如果为裁剪边，则为 `null`.
