---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.sliceRawPath()"
title: "static-sliceRawPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:29.962708Z"
selector: "article"
---

# static-sliceRawPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.sliceRawPath()

On this page

# MotionPathPlugin.sliceRawPath

### MotionPathPlugin.sliceRawPath( rawPath:Array, start:Number, end:Number ) : RawPath

Slices the provided RawPath Array at the designated start/end positions and returns the resulting (new, sliced) RawPath

#### Parameters

* #### **rawPath**: Array

  The RawPath Array to slice
* #### **start**: Number

  The position along the path at which to start, where 0 is the beginning and 1 is the end and 0.5 is the middle. It can be any positive or negative decimal number. For example, 0.3 would start the element at the 30% point along the curve. Default is 0.
* #### **end**: Number

  The position along the path at which to end, where 0 is the beginning, 1 is the end, and 0.5 is in the middle. It can be any positive or negative decimal number, including a value that's less than the start (which would make the object travel backwards). For example, 0.6 would have the element end at the 60% point along the curve. 1.5 would make it loop around back to the beginning and stop at the halfway point. Default is 1.

### Details[​](#details "Direct link to Details")

Slices the provided RawPath Array at the designated start/end positions and returns the resulting (new, sliced) RawPath

## What's a RawPath?[​](#whats-a-rawpath "Direct link to What's a RawPath?")

A RawPath is essentially an Array containing one Array for each contiguous segment with alternating x, y, x, y cubic bezier data. It's like an SVG`<path>`where there's one segment (Array) for each "M" command. That segment (Array) contains all of the cubic bezier coordinates in alternating x/y format (just like SVG path data) in raw numeric form which is nice because that way you don't have to parse a long string and convert things.

For example, this SVG `<path>` has two separate segments because there are two "M" commands and below is the resulting RawPath Array:

```
// original path (notice there are two "M" commands):  
(<path d="M0,0 C10,20,15,30,5,18 M0,100 C50,120,80,110,100,100" /)[  
  // resulting RawPath Array:  
  ([0, 0, 10, 20, 15, 30, 5, 18], [0, 100, 50, 120, 80, 110, 100, 100])  
];
```

For simplicity, the example above only has one cubic bezier in each segment, but there could be an unlimited quantity inside each segment. No matter what path commands are in the original`<path>`data string (cubic, quadratic, arc, lines, whatever), the resulting RawPath will **ALWAYS** be cubic beziers.