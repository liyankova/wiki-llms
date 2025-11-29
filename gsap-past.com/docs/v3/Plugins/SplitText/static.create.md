---
source_url: "https://gsap.com/docs/v3/Plugins/SplitText/static.create()"
title: "static-create | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:11.341334Z"
selector: "article"
---

# static-create | GSAP | Docs & Learning

* [SplitText](/docs/v3/Plugins/SplitText/)
* methods
* SplitText.create()

On this page

# SplitText.create

### SplitText.create( target: Element | String | Array, vars:Object ) : SplitText

Creates and returns a standalone SplitText instance

#### Parameters

* #### **vars**: Object

  An object containing all of the configuration details for the SplitText

### Returns : SplitText[​](#returns--splittext "Direct link to Returns : SplitText")

The new SplitText instance

### Details[​](#details "Direct link to Details")

Creates a new standalone SplitText instance.

## Example[​](#example "Direct link to Example")

```
SplitText.create(".headline", {  
  type: "lines,words",  
  linesClass: "line",  
  wordsClass: "word++",  
  autoSplit: true,  
  onSplit: (self) => {  
    return gsap.from(self.lines, {  
      yPercent: 100,  
      opacity: 0,  
      stagger: 0.1  
    });  
  }  
});
```

## Configuration[​](#configuration "Direct link to Configuration")

[see the main SplitText page.](/docs/v3/Plugins/SplitText/#config-object)