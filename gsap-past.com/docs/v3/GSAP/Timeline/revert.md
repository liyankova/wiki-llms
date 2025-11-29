---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/revert()"
title: "revert | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:47:14.171100Z"
selector: "article"
---

# revert | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .revert()

On this page

Added in v3.11.0

# revert

### revert( ) : Self

Reverts the Timeline and kills it, returning the targets to their pre-animation state including the removal of inline styles added by the Timeline.

### Returns : Self[​](#returns--self "Direct link to Returns : Self")

The Timeline itself, for easy chaining

### Details[​](#details "Direct link to Details")

Reverts the Timeline and kills it, returning the targets to their pre-animation state including the removal of inline styles added by the Timeline.

## The problem[​](#the-problem "Direct link to The problem")

What if you want to revert an element back to its state **BEFORE** it was animated? You could just `animation.progress(0)`, right? *Sort of*. Consider this element:

```
<div class="box"></div>
```

**No inline styles at all**. The opacity is 1 (the default) and then you do this:

```
// fade out  
let tl = gsap.timeline();  
tl.to(".box", { opacity: 0 });
```

Now let's try getting back to the original state:

```
tl.progress(0).pause();
```

That does indeed set it back to the starting values that GSAP parsed from the computed style:

```
<!-- inline style is still present -->  
<div class="box" style="opacity: 1"></div>
```

But that means **it** **still has inline styles**. Usually that doesn't matter, but perhaps a media query CSS rule sets opacity to 0.5 on that element. Doh! The inline style will overrule the class rule. So we need a way to have a tween/timeline keep track of the original inline styles and **REMOVE** the ones that it added. That requires a new method because `progress(0)` *SHOULD* set inline styles to ensure the state is what it's supposed to be at that point in the animation.

### The solution: revert()[​](#the-solution-revert "Direct link to The solution: revert()")

GSAP 3.11 added a `.revert()` method to all Tweens and Timelines, so it's as simple as:

```
tl.revert(); // removes inline styles that were added by the animation
```