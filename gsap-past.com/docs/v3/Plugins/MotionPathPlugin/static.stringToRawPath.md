---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.stringToRawPath()"
title: "static-stringToRawPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:33.236083Z"
selector: "article"
---

# static-stringToRawPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.stringToRawPath()

On this page

# MotionPathPlugin.stringToRawPath

### MotionPathPlugin.stringToRawPath( data:String ) : RawPath

#### Parameters

* #### **data**: String

  The string-based path data that should be converted to a RawPath. This is what is typically in the "d" attribute of an SVG path.

### Details[​](#details "Direct link to Details")

Converts a string of path data, like `"M0,0 C100,20 300,50 400,0..."` (which is what's typically found in the `d` attribute of a `<path>`) into a **RawPath**.

A **RawPath** is essentially an array containing an array for each contiguous segment with alternating x, y, x, y cubic bezier data. It's like an SVG `<path>` where there's one segment (array) for each `M` command. That segment (array) contains all of the cubic bezier coordinates in alternating x/y format (just like SVG path data) in raw numeric form which is nice because that way you don't have to parse a long string and convert things.

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

There is also a corresponding [`MotionPathPlugin.rawPathToString()`](/docs/v3/Plugins/MotionPathPlugin/static.rawPathToString()) method so that you can convert back and forth.