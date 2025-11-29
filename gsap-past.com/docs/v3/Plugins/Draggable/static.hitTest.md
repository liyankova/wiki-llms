---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/static.hitTest()"
title: "static-hitTest | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:12.474656Z"
selector: "article"
---

# static-hitTest | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* Draggable.hitTest()

On this page

# Draggable.hitTest

### Draggable.hitTest( testObject:Object, threshold:[Number | String] ) : Boolean

Provides an easy way to test whether or not the target element overlaps with a particular element (or the mouse position) according to whatever threshold you [optionally] define.

#### Parameters

* #### **testObject**: Object

  The object that should be hit tested, which can be any of the following: an element, a mouse/touch event that has `pageX` and `pageY` properties, selector text like `"#element2"`, or a generic object defining a rectangle (it should have `top, left, right,` and `bottom` properties).
* #### **threshold**: [Number | String]

  (default = `0`) - Either a number defining the minimum number of pixels that must be overlapping for a positive hitTest or a string percentage (like `"50%"`) defining the minimum amount of overlapping surface area percentage for a positive hitTest. Zero (0) will check for any overlap at all.

### Returns : Boolean[​](#returns--boolean "Direct link to Returns : Boolean")

Returns `true` if an overlap is sensed (according to the threshold), `false` otherwise.

#### loading...

### Details[​](#details "Direct link to Details")

Provides an easy way to test whether or not the `target` element overlaps with a particular element (or the mouse position) according to whatever `threshold` you (optionally) define. For example:

```
Draggable.create("#element1", {      
  type: "x,y",      
  onDragEnd: function(e) {          
    //see if the target overlaps with the element with ID "element2"         
    if (this.hitTest("#element2")) {              
    //do stuff         
    }      
  }  
});
```

By default, `hitTest()` returns true if there is any overlap whatsoever, but you can optionally define a `threshold` parameter to, for example, only return true if at least 20 pixels are overlapping or if 50% of the surface area of either element is overlapping with the other or whatever amount you define:

```
Draggable.create("#element1", {      
  type: "x,y",      
  onDragEnd: function(e) {          
    //checks if at least 20 pixels are overlapping:          
    if (this.hitTest("#element2", 20)) {              
      //do stuff          
    }         
    //checks if at least 50% of the surface area of either element is overlapping:          
    if (this.hitTest("#element3", "50%")) {              
      //do stuff          
    }     
  }  
});
```

#### loading...

You can use `hitTest(window)` to detect if an element is visible within the viewport.

There is also a static version of this method that allows you to pass both elements and objects to test, like `Draggable.hitTest(element1, element2, 20)`. [Demo](https://codepen.io/GreenSock/pen/ZOayGO?editors=0010).

**IMPORTANT:** There is no way to get pixel-perfect hit testing for non-rectangular shapes in the DOM. `hitTest()` uses the browser's `getBoundingClientRect()` method to get the rectangular bounding box that surrounds the entire element, thus if you rotate an element or if it's more of a circular shape, the bounding box may extend further than the visual edges.