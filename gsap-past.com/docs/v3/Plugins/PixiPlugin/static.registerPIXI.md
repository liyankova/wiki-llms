---
source_url: "https://gsap.com/docs/v3/Plugins/PixiPlugin/static.registerPIXI()"
title: "static-registerPIXI | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:56.263478Z"
selector: "article"
---

# static-registerPIXI | GSAP | Docs & Learning

* more plugins
* [Pixi](/docs/v3/Plugins/PixiPlugin/)
* methods
* PixiPlugin.registerPIXI()

On this page

# PixiPlugin.registerPIXI

### PixiPlugin.registerPIXI( PIXI:Object ) ;

Registers the main PIXI library object with the PixiPlugin so that it can find the necessary classes/objects. You only need to register it once.

#### Parameters

* #### **PIXI**: Object

  The main PIXI library object

### Details[​](#details "Direct link to Details")

PixiPlugin needs some reference to the PIXI library object (usually `PIXI`), which it looks for in the global scope (`window` in most cases). However in a build system or ES module environment you might not have a global scope that has a reference to your `PIXI` object. That's where this method is useful. You can simply pass in that reference using this method like:

```
PixiPlugin.registerPIXI(PIXI);
```

When importing the entire Pixi.js library, you can register Pixi like this:

```
import { gsap } from "gsap";  
import { PixiPlugin } from "gsap/PixiPlugin";  
import * as PIXI from "pixi.js";  
  
gsap.registerPlugin(PixiPlugin);  
PixiPlugin.registerPIXI(PIXI);
```

When importing individual Pixi.js modules, you can pass in the plugin's dependencies as an object.

* **Container**: (required)
* **Sprite**: (optional) Needed to render a textured object
* **filters**: (optional) Needed to animate `ColorMatrixFilter` and `BlurFilter` properties

```
import { gsap } from "gsap";  
import { PixiPlugin } from "gsap/PixiPlugin";  
  
import { Container, Sprite, BlurFilter, ColorMatrixFilter } from "https://cdn.skypack.dev/pixi.js";  
  
PixiPlugin.registerPIXI({  
  Container,  
  Sprite,  
  BlurFilter,  
  ColorMatrixFilter  
});
```