---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/revert()"
title: "revert | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:46.213655Z"
selector: "article"
---

# revert | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .revert()

On this page

# revert

### revert( ) : Self

Reverts the animation and kills it, returning the targets to their pre-animation state including the removal of inline styles added by the animation.

### Returns : Self[​](#returns--self "Direct link to Returns : Self")

The Tween itself, for easy chaining

### Details[​](#details "Direct link to Details")

Reverts the animation and kills it, returning the targets to their pre-animation state including the removal of inline styles added by the animation.

## The problem[​](#the-problem "Direct link to The problem")

What if you want to revert an element back to its state **BEFORE** it was animated? You could just `animation.progress(0)`, right? *Sort of*. Consider this element:

```
<div class="box"></div>
```

**No inline styles at all**. The opacity is 1 (the default) and then you do this:

```
// fade out  
let tween = gsap.to(".box", { opacity: 0 });
```

Now let's try getting back to the original state:

```
tween.progress(0).pause();
```

That does indeed set it back to the starting values that GSAP parsed from the computed style:

```
<!-- inline style is still present -->  
<div class="box" style="opacity: 1"></div>
```

But that means **it** **still has inline styles**. Usually that doesn't matter, but perhaps a media query CSS rule sets opacity to 0.5 on that element. Doh! The inline style will overrule the class rule. So we need a way to have a tween/timeline keep track of the original inline styles and **REMOVE** the ones that it added. That requires a new method because `progress(0)` *SHOULD* set inline styles to ensure the state is what it's supposed to be at that point in the animation.

### The solution: animation.revert()[​](#the-solution-animationrevert "Direct link to The solution: animation.revert()")

GSAP 3.11 added a `.revert()` method to all Tweens and Timelines, so it's as simple as:

```
animation.revert(); // removes inline styles that were added by the animation
```