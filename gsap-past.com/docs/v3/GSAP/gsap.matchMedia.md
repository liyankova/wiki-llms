---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.matchMedia()"
title: "gsap.matchMedia() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:41:20.515352Z"
selector: "article"
---

# gsap.matchMedia() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.matchMedia()

On this page

### Returns : MatchMedia[​](#returns--matchmedia "Direct link to Returns : MatchMedia")

Detailed walkthrough

Responsive, accessible animations and ScrollTriggers, here you come! 🥳 `gsap.matchMedia()` lets you tuck setup code into a function that only executes when a particular [media query](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) matches and then when it no longer matches, all the GSAP animations and [ScrollTriggers](/docs/v3/Plugins/ScrollTrigger) created during that function's execution get **reverted automatically**! Customizing for mobile/desktop or `prefers-reduced-motion` accessibility is remarkably simple.

Each [media query string](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) is exactly what you'd pass into the browser's native [window.matchMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList#Examples)

## Basic syntax[​](#basic-syntax "Direct link to Basic syntax")

```
// create  
let mm = gsap.matchMedia();  
  
// add a media query. When it matches, the associated function will run  
mm.add("(min-width: 800px)", () => {  
  
  // this setup code only runs when viewport is at least 800px wide  
  gsap.to(...);  
  gsap.from(...);  
  ScrollTrigger.create({...});  
  
  return () => { // optional  
    // custom cleanup code here (runs when it STOPS matching)  
  };  
});  
  
// later, if we need to revert all the animations/ScrollTriggers...  
mm.revert();
```

We create a `mm` variable for the MatchMedia so that we can `add()` as many media queries as we want to that one object. That way, we have a single object on which we can call `revert()` to instantly revert all the animations/ScrollTriggers that were created in any of the associated MatchMedia functions.

The function gets invoked whenever it becomes active (matches). So if a user resizes the browser past the breakpoint and back again multiple times, the function would get called multiple times.

### .add() parameters[​](#add-parameters "Direct link to .add() parameters")

1. **query/conditions** - a [media query string](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) like `"(min-width: 800px)"`**-OR-** a [conditions object](#conditions) with as many arbitrarily-named query strings as you'd like; you'll be able to check the matching status of each (boolean). See [below](#conditions) for details about the conditions syntax.
2. **handler function** - the function to invoke when there's a match. All GSAP animations and ScrollTriggers created during execution of this function will be collected in the context so that they can be reverted when the MatchMedia gets reverted (like when the condition stops matching).
3. **scope** *[optional]* - all GSAP-related selector text inside the handler function will be scoped to this Element or [React Ref](https://reactjs.org/docs/refs-and-the-dom.html) or [Angular ElementRef](https://angular.io/api/core/ElementRef). Think of it like calling `querySelectorAll()` on this element, so only its descendants can be selected. See [below](#scope) for details.

So the structure looks like:

```
mm.add("(min-width: 800px)", () => {...}, myElementOrRef);
```

### Simplistic desktop/mobile example[​](#simplistic-desktopmobile-example "Direct link to Simplistic desktop/mobile example")

```
let mm = gsap.matchMedia();  
  
mm.add("(min-width: 800px)", () => {  
  // desktop setup code here...  
});  
  
mm.add("(max-width: 799px)", () => {  
  // mobile setup code here...  
});
```

## Conditions syntax[​](#conditions "Direct link to Conditions syntax")

What if your setup code for various media queries is mostly identical but a few key values are different? If you `add()` each media query individually, you may end up with a lot of **redundant code**. Just use the conditions syntax! Instead of a string for the first parameter, use an **object with arbitrarily-named conditions** and then the function will get called when **any** of those conditions match and you can check each condition as a boolean (matching or not). The conditions object could look like this:

```
{  
  isDesktop: "(min-width: 800px)",  
  isMobile: "(max-width: 799px)",  
  reduceMotion: "(prefers-reduced-motion: reduce)"  
}
```

Name your conditions whatever you want.

Below we'll set the breakpoint at 800px wide and honor the user's `prefers-reduced-motion` preference, leveraging the same setup code and using conditional logic where necessary:

```
let mm = gsap.matchMedia(),  
  breakPoint = 800;  
  
mm.add(  
  {  
    // set up any number of arbitrarily-named conditions. The function below will be called when ANY of them match.  
    isDesktop: `(min-width: ${breakPoint}px)`,  
    isMobile: `(max-width: ${breakPoint - 1}px)`,  
    reduceMotion: "(prefers-reduced-motion: reduce)",  
  },  
  (context) => {  
    // context.conditions has a boolean property for each condition defined above indicating if it's matched or not.  
    let { isDesktop, isMobile, reduceMotion } = context.conditions;  
  
    gsap.to(".box", {  
      rotation: isDesktop ? 360 : 180, // spin further if desktop  
      duration: reduceMotion ? 0 : 2, // skip to the end if prefers-reduced-motion  
    });  
  
    return () => {  
      // optionally return a cleanup function that will be called when none of the conditions match anymore (after having matched)  
      // it'll automatically call context.revert() - do NOT do that here . Only put custom cleanup code here.  
    };  
  }  
);
```

Nice and concise! 🎉

It will revert and run the handler function again if/when **any** of the conditions toggle (it won't run again if none of them match, of course). For example, if you have three conditions and two of them match, it will run. Then if one of the matching queries *STOPS* matching (toggles to `false`), it'll revert and run the function again with updated condition values.

Notice that [Context](/docs/v3/GSAP/gsap.context()) is created and passed in as the only parameter. This can be useful if you need to create event handlers or execute other code later that creates animations/ScrollTriggers which should be reverted when `revert()` is called on the MatchMedia.

## Demo using conditional syntax[​](#demo-using-conditional-syntax "Direct link to Demo using conditional syntax")

#### loading...

## Interactivity and cleanup[​](#interactivity-and-cleanup "Direct link to Interactivity and cleanup")

The GSAP animations and ScrollTriggers created while the function is executed get recorded in the [Context](/docs/v3/GSAP/gsap.context()), but what if you set up event listeners, like for "click" events which run sometime later, **after** the MatchMedia function is done executing? You can add() a named function to the Context object itself so that when it runs, any animations/ScrollTriggers created in that function get collected in the Context, like:

```
let mm = gsap.matchMedia();  
  
mm.add("(min-width: 800px)", (context) => {  
  context.add("onClick", () => {  
    gsap.to(".box", { rotation: 360 }); // <- now it gets recorded in the Context  
  });  
  
  myButton.addEventListener("click", context.onClick);  
  
  return () => {  
    // make sure to clean up event listeners in the cleanup function!  
    myButton.removeEventListener("click", context.onClick);  
  };  
});
```

## Scoping selector text[​](#scope "Direct link to Scoping selector text")

You can optionally pass in an Element or [React Ref](https://reactjs.org/docs/refs-and-the-dom.html) or [Angular ElementRef](https://angular.io/api/core/ElementRef) as the 3rd parameter and then **all** the selector text in the supplied function will be scoped to that particular Element/Ref (like calling `querySelectorAll()` on that Element/Ref).

```
let mm = gsap.matchMedia();  
  
mm.add("(min-width: 800px)", () => {  
  
  gsap.to(".box", {...}) // <- normal selector text, automatically scoped to myRefOrElement  
  
}, myRefOrElement); // <- scope!!!
```

The `scope` can be selector text itself like `".myClass"`, or an Element, React Ref or Angular ElementRef.

Set a **default scope** when you create the MatchMedia by passing it in as the only parameter:

```
let mm = gsap.matchMedia(myRefOrElement);  
  
mm.add("(min-width: 800px)", () => {  
  
  // selector text scoped to myRefOrElement  
  gsap.to(".class", {...});  
  
});  
  
mm.add("(max-width: 799px)", () => {  
  
  // selector text scoped to myOtherElement  
  gsap.to(".class", {...});  
  
}, myOtherElement); // <- overrides default scope!!!
```

## Refreshing all matches[​](#refreshing-all-matches "Direct link to Refreshing all matches")

Use [gsap.matchMediaRefresh()](/docs/v3/GSAP/gsap.matchMediaRefresh()) to immediately revert all active/matching MatchMedia objects and then run any that currently match. This can be very useful if you need to accommodate a UI checkbox that toggles a reduced motion preference, for example.

## Accessible animations with prefers-reduced-motion[​](#accessible-animations-with-prefers-reduced-motion "Direct link to Accessible animations with prefers-reduced-motion")

We all love animation here, but it can make some users with vestibular disorders feel nauseous. It's important to respect their preferences and either serve up minimal animation, or no animation at all. We can tap into the prefers reduced motion media query for this

### simple demo[​](#simple-demo "Direct link to simple demo")

#### loading...

### checkbox toggle[​](#checkbox-toggle "Direct link to checkbox toggle")

#### loading...

[More information in this CSS tricks article](https://css-tricks.com/empathetic-animation/)

## Do I need to use gsap.context()?[​](#do-i-need-to-use-gsapcontext "Direct link to Do I need to use gsap.context()?")

Nope! Internally, gsap.matchMedia() creates a [gsap.context()](/docs/v3/GSAP/gsap.context()), so it would be redundant and completely unnecessary to use both. Think of gsap.matchMedia() like a specialized wrapper around [gsap.context()](/docs/v3/GSAP/gsap.context()). So when you call `revert()` on the gsap.matchMedia() object, it's the same thing as calling it on the [gsap.context()](/docs/v3/GSAP/gsap.context()).

## Examples[​](#examples "Direct link to Examples")

See the [CodePen Collection](https://codepen.io/collection/vBebgJ)

### Mobile device doesn't seem to work?[​](#mobile-device-doesnt-seem-to-work "Direct link to Mobile device doesn't seem to work?")

Try adding this in your `<head></head>`:

```
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

gsap.matchMedia() was added in GSAP **3.11.0.**