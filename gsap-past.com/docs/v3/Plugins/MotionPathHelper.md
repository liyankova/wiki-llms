---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathHelper/"
title: "MotionPathHelper | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:45:06.524418Z"
selector: "article"
---

# MotionPathHelper | GSAP | Docs & Learning

* more plugins
* MotionPathHelper

On this page

MotionPathHelper lets you **interactively edit a motion path directly in the browser** by dragging its anchors and control points, adding/deleting them, or dragging the entire path! If you don't have a motion path yet, you can create a new one from scratch. Once you're done editing, simply click the big "COPY MOTION PATH" button at the bottom of the screen to have the path data string copied to your clipboard so that you can then paste it directly into your tween or an SVG `<path>` that you'll use for the motion path animation.

Without MotionPathHelper, you'd need to go back and forth between the browser and an SVG editor like Inkscape or Adobe Illustrator which is time-consuming and frustrating.

## Video[​](#video "Direct link to Video")

info

The video below explains [MotionPathPlugin](/docs/v3/Plugins/MotionPathPlugin), and shows MotionPathHelper around 3:18:

## Usage[​](#usage "Direct link to Usage")

Call `MotionPathHelper.create()` and pass it either of the following:

* **A [Tween](/docs/v3/GSAP/Tween) instance that has a motionPath defined**. In this case, it will grab the motion path from the Tween and make it editable in the browser. For example:

  ```
  const tween = gsap.to("#id", {  
    motionPath: {  
      path: "#path",  
      align: "#path",  
      alignOrigin: [0.5, 0.5],  
    },  
  });  
    
  // pass the tween instance in here...  
  MotionPathHelper.create(tween);
  ```
* **An element (or selector text)**. In this case, it will create a new very basic motion path curve that you can start editing. For example:

  ```
  // just pass the element or selector text:  
  MotionPathHelper.create("#id");
  ```

## **Config Object**[​](#config-object "Direct link to config-object")

You can optionally pass in a `vars` parameter to further configure the motion path helper. It's an object and can include any of the following properties:

### Property

### Description

* #### ease

  Number - The ease to use for the looping preview animation.
* #### duration

  Number - The duration of the looping preview animation (each iteration)
* #### path

  String | Element | Array The motion path along which to animate the target(s). This can be a direct reference to a  or selector text or path data like "M9,100c0,0,18-41,49-65" or an Array of points through which the path should be plotted.
* #### pathColor

  String - The color of the path stroke (only applies if no `path` is defined and MotionPathHelper must create one).
* #### pathWidth

  Number - The stroke-width of the path (only applies if no `path` is defined and MotionPathHelper must create one).
* #### pathOpacity

  Number - The opacity of the path stroke (only applies if no `path` is defined and MotionPathHelper must create one).
* #### selected

  Boolean - Whether or not the path will be selected initially.
* #### start

  Number - The position along the path at which to start, where 0 is the beginning and 1 is the end and 0.5 is the middle. It can be any positive or negative decimal number. For example, `0.3` would start the element at the 30% point along the curve. Default is 0. This only applies if there is no existing animation that the MotionPathHelper is showing.
* #### end

  Number - The position along the path at which to end, where 0 is the beginning, 1 is the end, and 0.5 is in the middle. It can be any positive or negative decimal number, including a value that's less than the start (which would make the object travel backwards). For example, `0.6` would have the element end at the 60% point along the curve. 1.5 would make it loop around back to the beginning and stop at the halfway point. Default is 1. This only applies if there is no existing animation that the MotionPathHelper is showing.

## Sample code[​](#sample-code "Direct link to Sample code")

```
MotionPathHelper.create("#elementID", {  
  path: "#path",  
  pathWidth: 5,  
  pathColor: "red",  
  pathOpacity: 0.6,  
  selected: true,  
  start: 0.1,  
  end: 1,  
  duration: 5,  
  ease: "power2.inOut",  
});
```

## Demo[​](#demo "Direct link to Demo")

#### loading...

tip

## Editing tips[​](#editing-tips "Direct link to Editing tips")

* **Add point**: ALT-Click somewhere on the path
* **Toggle smooth/corner anchor**: ALT-Click the anchor
* **Get handle from corner anchor**: ALT-Drag
* **Select multiple anchors**: SHIFT-Click (and again to deselect)
* **Delete anchor**: select it, then press DELETE key.
* **Undo**: CTRL-Z
* Click and drag on handles to change how the path curves.
* **Drag entire path**: Click and drag on a part of the path that doesn't have an anchor

warning

MotionPathHelper requires [MotionPathPlugin](/docs/v3/Plugins/MotionPathPlugin). Don't forget to load and register both plugins.

## **Methods**[​](#methods "Direct link to methods")

|  |  |
| --- | --- |
| [kill](/docs/v3/MotionPathHelper/kill())( ) ; | Kills the MotionPathHelper instance, removing the path editing elements and "Copy" button from the DOM. |
| [MotionPathHelper.editPath](/docs/v3/MotionPathHelper/static.editPath())( path:Element | String, config:Object ) : PathEditor | Makes an SVG `<path>` editable in the browser. |