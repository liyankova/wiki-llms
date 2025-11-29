---
source_url: "https://gsap.com/docs/v3/MotionPathHelper/static.editPath()"
title: "static-editPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:38.576647Z"
selector: "article"
---

# static-editPath | GSAP | Docs & Learning

* more plugins
* [MotionPathHelper](/docs/v3/Plugins/MotionPathHelper)
* methods
* MotionPathHelper.editPath()

On this page

# MotionPathHelper.editPath

### MotionPathHelper.editPath( path:Element | String, config:Object ) : PathEditor

Makes an SVG `<path>` editable in the browser.

#### Parameters

* #### **path**: Element | String

  The <path> element to be edited. This can be a reference to the element or selector text.
* #### **config**: Object

  An optional configuration object for defining things like onPress, onRelease, handleSize, selected, draggable, etc.

### Returns : PathEditor[​](#returns--patheditor "Direct link to Returns : PathEditor")

A PathEditor object

### Details[​](#details "Direct link to Details")

Makes an SVG `<path>` editable in the browser.

## Simple example[​](#simple-example "Direct link to Simple example")

```
MotionPathHelper.editPath("#my-path");
```

## Advanced example[​](#advanced-example "Direct link to Advanced example")

```
MotionPathHelper.editPath("#my-path", {  
  handleSize: 7,  
  selected: true,  
  draggable: true,  
  onPress: () => console.log("pressed"),  
  onRelease: () => console.log("released"),  
  onUpdate: () => console.log("updated"),  
  onDeleteAnchor: () => console.log("deleted anchor"),  
});
```

## Demo[​](#demo "Direct link to Demo")

#### loading...

### Configuration[​](#configuration "Direct link to Configuration")

You can optionally pass in a `vars` parameter to further configure the path editor. It's an object and can include any of the following properties:

| Property | Description |
| --- | --- |
| draggable | Boolean - determines if the path should be selected initially. |
| handleSize | Number - The radius of the anchor points/handles |
| onDeleteAnchor | Function - A callback function that should be called when an anchor point is deleted. |
| onPress | Function - A callback function that should be called when an anchor or the path is pressed (mousedown/pointerdown/touchstart) |
| onRelease | Function - A callback function that should be called when the mouse/pointer is released (mouseup/pointerup/touchend/touchcancel) |
| onUpdate | Function - A callback function that should be called when the path is updated in any way |
| selected | Boolean - Whether or not the path will be selected initially. |

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