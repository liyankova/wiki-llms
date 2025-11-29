---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.arrayToRawPath()"
title: "static-arrayToRawPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:03.356658Z"
selector: "article"
---

# static-arrayToRawPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.arrayToRawPath()

On this page

# MotionPathPlugin.arrayToRawPath

### MotionPathPlugin.arrayToRawPath( values:Array, vars:Object ) : RawPath Array

Takes an Array of coordinates and plots a curve through them, returning a corresponding RawPath Array. If `type: "cubic"` is declared in the `vars` parameter object, they will be interpreted as cubic bezier points like anchor, two control points, anchor, two control points, anchor, etc.)

#### Parameters

* #### **values**: Array

  An Array of points through which to plot a curve (or if `type: "cubic"` is declared in the `vars` parameter object, they will be interpreted as cubic bezier points like anchor, two control points, anchor, two control points, etc.)
* #### **vars**: Object

  [optional] Configuration object that can contain properties like "curviness", "relative", "type", "x", or "y"

### Details[​](#details "Direct link to Details")

Takes an Array of coordinates and plots a curve through them, returning a corresponding RawPath Array. If `type: "cubic"` is declared in the `vars` parameter object, they will be interpreted as cubic bezier points like anchor, two control points, anchor, two control points, anchor, etc.)

## Configuration[​](#configuration "Direct link to Configuration")

The `vars` parameter is optional and can contain any of the following:

| Property | Description |
| --- | --- |
| curviness | Number - A number that sets the curviness of a path generated. 1 is the default, 2 would be more curvy. Default is 1. |
| type | String - There are two options for the type: "thru" and "cubic". When "thru" is used, all points are considered to be anchor points and a curve will be plotted through them. When "cubic" is used, the points are interpreted as cubic bezier points in the following order: anchor, two control points, anchor, two control points, etc. for as many iterations as you want but obviously make sure that it starts and ends with anchors. |
| relative | Boolean - If true, each successive value is interpreted as relative to the previous one. For example, if the Array is `[{x:5}, {x:10}, {x:-2}]`, it would first move to 105, then 115, and finally end at 113. |
| x | String - By default, "x" is used as the horizontal property value but you can set it to something else like "left" if you prefer, like `{x: "left"}`. |
| y | String - By default, "y" is used as the vertical property value but you can set it to something else like "top" if you prefer, like `{y: "top"}`. |

## What's a RawPath?[​](#whats-a-rawpath "Direct link to What's a RawPath?")

A **RawPath** is essentially an Array containing an Array for each contiguous segment with alternating x, y, x, y cubic bezier data. It's like an SVG `<path>` where there's one segment (Array) for each "M" command. That segment (Array) contains all of the cubic bezier coordinates in alternating x/y format (just like SVG path data) in raw numeric form which is nice because that way you don't have to parse a long string and convert things.

For example, this SVG `<path>` has two separate segments because there are two "M" commands:

```
<path d="M0,0 C10,20,15,30,5,18 M0,100 C50,120,80,110,100,100" />
```

The resulting RawPath would be:

```
[  
  [0, 0, 10, 20, 15, 30, 5, 18],  
  [0, 100, 50, 120, 80, 110, 100, 100],  
];
```

For simplicity, the example above only has one cubic bezier in each segment, but there could be an unlimited quantity inside each segment. No matter what path commands are in the original`<path>` data string (cubic, quadratic, arc, lines, whatever), the resulting RawPath will **ALWAYS** be cubic beziers.

## Sample code[​](#sample-code "Direct link to Sample code")

```
let anchors = [  
    { x: 50, y: 130 },  
    { x: 300, y: 10 },  
    { x: 510, y: 100 },  
    { x: 700, y: 190 },  
    { x: 850, y: 100 },  
  ],  
  rawPath = MotionPathPlugin.arrayToRawPath(anchors, { curviness: 0.5 }),  
  path = document.querySelector("#path");  
  
path.setAttribute("d", MotionPathPlugin.rawPathToString(rawPath));
```

## Demo[​](#demo "Direct link to Demo")

#### loading...