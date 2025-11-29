---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.getRawPath()"
title: "static-getRawPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:19.531748Z"
selector: "article"
---

# static-getRawPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.getRawPath()

On this page

# MotionPathPlugin.getRawPath

### MotionPathPlugin.getRawPath( value:String | Element ) : RawPath (Array)

Gets the RawPath (Array) for the provided element or raw SVG <path> data. A RawPath is essentially an Array containing one Array for each contiguous segment with alternating x, y, x, y cubic bezier data.

#### Parameters

* #### **value**: String | Element

  Selector text, Element reference, or raw SVG <path> data from which to get the RawPath Array. For example, "#path", myPath, or "M9,100c0,0,18-41,49-65".

### Details[​](#details "Direct link to Details")

Gets the RawPath (Array) for the provided element or raw SVG`<path>`data.

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