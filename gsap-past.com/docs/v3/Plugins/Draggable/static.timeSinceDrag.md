---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/static.timeSinceDrag()"
title: "static-timeSinceDrag | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:18.927738Z"
selector: "article"
---

# static-timeSinceDrag | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* Draggable.timeSinceDrag()

On this page

# Draggable.timeSinceDrag

### Draggable.timeSinceDrag( ) : Number

Returns the time (in seconds) that has elapsed since the last drag ended.

### Returns : Number[​](#returns--number "Direct link to Returns : Number")

The time (in seconds) since the last drag ended.

### Details[​](#details "Direct link to Details")

Returns the time (in seconds) that has elapsed since the last drag ended - this can be useful in situations where you want to skip certain actions if a drag just occurred. For example, imagine a draggable `<div>` with a bunch of child elements that have `onclick` handlers - if the user clicks on of those and drags the whole `<div>` and then releases, you might want to ignore that "click" because the user was intending to drag, not click (don't forget to set `dragClickables: true` in the Draggable):

```
$("#myDiv a").click(function(e) {    if (Draggable.timeSinceDrag() > 0.2) {        //do stuff, but not if the user just dragged within the last 0.2 seconds    }});
```

There is also a `timeSinceDrag()` instance method.

```
myDraggable.timeSinceDrag();
```