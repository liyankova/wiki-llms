---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/addEventListener()"
title: "addEventListener | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:52.144247Z"
selector: "article"
---

# addEventListener | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* .addEventListener()

On this page

# addEventListener

### addEventListener( ) ;

### Details[​](#details "Direct link to Details")

Registers a function that should be called each time a particular type of event occurs. Inside the listener function `this` refers to the target of the Draggable instance that fired the event.

## Events[​](#events "Direct link to Events")

* press
* click
* dragstart
* drag
* dragend
* release
* throwcomplete
* throwupdate

## Usage[​](#usage "Direct link to Usage")

```
var myDraggable = Draggable.create("#box1", {  bounds: "#container"})[0];myDraggable.addEventListener("press", onPress);function onPress() {  console.log("myDraggable was pressed");  gsap.to(this, {duration: 0.2, backgroundColor: "red"}); // animate the backgroundColor of the target of the Draggable that was pressed}
```