---
layout: docs
menu: docs
title: Axis
permalink: /docs/axis.html
---

Axes provide axis lines, ticks, and labels to convey how a positional range represents a data range. Simply put, axes visualize scales.

By default, Vega-Lite automatically creates axes with default properties for `x` and `y` channels when they encode data fields. User can set the `axis` property of x- or y-[field definition](encoding.html#field) to an object to customize [axis properties](#axis-properties) or set `axis` to `null` to remove the axis.

Besides `axis` property of a field definition, the configuration object ([`config`](config.html)) also provides [axis config](#config) (`config: {axis: {...}}`) for setting default axis properties for all axes.

<!--prettier-ignore-start-->
## Documentation Overview
{:.no_toc}

- TOC
{:toc}

<!--prettier-ignore-end-->

## Axis Properties

```js
// A Single View or a Layer Specification
{
  ...,
  "mark/layer": ...,
  "encoding": {
    "x": {
      "field": ...,
      "type": ...,
      "axis": {                // Axis
        ...
      },
      ...
    },
    "y": ...,
    ...
  }
}
```

{:#properties}

To customize axis, you can specify an `axis` object in [an encoding channel's definition](encoding.html). This section lists all properties of axes.

_See also:_ This [interactive article](https://beta.observablehq.com/@jheer/a-guide-to-guides-axes-legends-in-vega) demonstrates axes and legends in the underlying Vega language.

{:#general}

### General

{% include table.html props="bandPosition,maxExtent,minExtent,orient,offset,position,translate,zindex" source="Axis" %}

#### Example: Using Axis `minExtent` to Align Multi-View Plots

By default, Vega-Lite automatically sets the axis extent (the space axis ticks and labels use). However, to align axes between multiple plots in multi-view displays, you can manually set `minExtent` (and optionally `maxExtent`) to make the extent consistent across plots.

<div class="vl-example" data-name="nested_concat_align"></div>

{:#domain}

### Domain

{% include table.html props="domain,domainColor,domainOpacity,domainWidth" source="Axis" %}

{:#labels}

### Labels

{% include table.html props="format,formatType,labels,labelAlign,labelAngle,labelBaseline,labelBound,labelColor,labelExpr,labelFlush,labelFlushOffset,labelFont,labelFontSize,labelFontStyle,labelFontWeight,labelLimit,labelOpacity,labelOverlap,labelPadding,labelSeparation" source= "Axis" %}

**See also:** [`guide-label` style config](mark.html#style-config) (common styles for axis, [legend](legend.html), and [header](facet.html#header) labels).

#### Example: Using Axis `labelExpr` to Display Initial Letters of Month Name

<div class="vl-example" data-name="bar_month_temporal_initial"></div>

{:#ticks}

### Ticks

{% include table.html props="ticks,tickBand,tickColor,tickCount,tickDash,tickExtra,tickMinStep,tickOffset,tickOpacity,tickRound,tickSize,tickWidth,values" source="Axis" %}

{:#title}

### Title

{% include table.html props="title,titleAlign,titleAnchor,titleAngle,titleBaseline,titleColor,titleFont,titleFontSize,titleFontStyle,titleFontWeight,titleLimit,titleOpacity,titlePadding,titleX,titleY" source="Axis" %}

For example, the following plot has a customized x-axis title.

<div class="vl-example" data-name="bar_1d"></div>

**See also:** [Axis Title Config](#title-config) and [`guide-title` style config](mark.html#style-config) (common styles for axis, [legend](legend.html), and [header](facet.html#header) titles).

### Grid

{% include table.html props="grid,gridColor,gridDash,gridOpacity,gridWidth" source="Axis" %}

<!--
### Custom Axis Encodings

**TODO** (We have `encoding` property akin to [Vega's axis `encode`](https://vega.github.io/vega/docs/axes/#custom-axis-encodings), but within each element's block, we do not have `enter/update/exit`.)
-->

{:#conditional}

### Conditional Axis Properties

We can set axis properties (which can be of type "ConditionalAxisProperty") to a [conditional value definition](condition.html#value).

Note that each axis tick, grid line, and label instance is backed by a data object with the following fields, which may be accessed as part of the test condition in a condition axis property.

- `label` - the string label
- `value` - the data value

For example, we can adjust the grid dash in a line chart based on whether a particular grid line falls on a year boundary:

<div class="vl-example" data-name="line_conditional_grid_dash"></div>

We can also conditionally hide some labels and ticks in the following Lasagna plot using conditional `labelColor` and `tickColor`:

<div class="vl-example" data-name="rect_lasagna"></div>

{:#config}

## Axis Config

```js
// Top-level View Specification
{
  ...
  "config": {
    "axis": : ...,
    "axisX": : ...,
    "axisY": : ...,
    "axisLeft": : ...,
    "axisRight": : ...,
    "axisTop": : ...,
    "axisBottom": : ...,
    "axisBand": : ...,
    ...
  }
}
```

Axis configuration defines default settings for axes. Properties defined under the `"axis"` property in the top-level [`config`](config.html) object are applied to _all_ axes.

Additional property blocks can target more specific axis types based on the orientation (`"axisX"`, `"axisY"`, `"axisLeft"`, `"axisTop"`, etc.) or band scale type (`"axisBand"`). For example, properties defined under the `"axisBand"` property will only apply to axes visualizing `"band"` scales. If multiple axis config blocks apply to a single axis, type-based options take precedence over orientation-based options, which in turn take precedence over general options.

An axis configuration supports all [axis properties](#properties) except `position`, `orient`, `format`, `tickCount`, `values`, and `zindex`.

The `shortTimeLabels` property is also available for the general axis config (`config.axis`), but not for specific axis config (e.g., `config.axisX`).

{% include table.html props="shortTimeLabels" source="AxisConfig" %}

**See also:** [Axis Labels Properties](#labels) and [`guide-label` style config](mark.html#style-config) (common styles for by axis, [legend](legend.html), and [header](facet.html#header) labels).

<!-- hide as `grid` in axis config does not work yet.
### Axis Config Example

Setting axis config's `domain` and `grid` to `false` hides all axis domain lines and grids.

<div class="vl-example" data-name="point_no_axis_domain_grid"></div> -->
