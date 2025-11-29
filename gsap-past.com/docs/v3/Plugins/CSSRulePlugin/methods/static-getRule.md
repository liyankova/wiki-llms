---
source_url: "https://gsap.com/docs/v3/Plugins/CSSRulePlugin/methods/static-getRule()"
title: "static-getRule() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:42.274065Z"
selector: "article"
---

# static-getRule() | GSAP | Docs & Learning

* more plugins
* [CSSRule](/docs/v3/Plugins/CSSRulePlugin/)
* methods
* CSSRulePlugin.getRule()

On this page

# CSSRulePlugin.getRule

### CSSRulePlugin.getRule( selector:String ) : Object

[static] Provides a simple way to find the style sheet object associated with a particular selector like `".myClass"` or `"#myID"`.

#### Parameters

* #### **selector**: String

  The name that exactly matches the selector you want to animate (like `".myClassName"`).

### Returns : Object[​](#returns--object "Direct link to Returns : Object")

The stylesheet object (or an array of them if you define only a pseudo element selector like `::before`).

### Details[​](#details "Direct link to Details")

Provides a simple way to find the style sheet object associated with a particular selector like `.myClass` or `#myID`. You'd use this method to determine the target of your tween.

For example, let's say you have CSS like this:

```
.myClass {  
  color: #FF0000;  
}  
.myClass::before {  
  content: "This content is before.";  
  color: #00FF00;  
}
```

And you want to tween the color of the `.myClass::before` to `blue`. Make sure you load the CSSRulePlugin.js file and then you can do this:

```
var rule = CSSRulePlugin.getRule(".myClass::before"); //get the rule  
gsap.to(rule, {duration: 3, cssRule: {color: "#0000FF"}});
```

Or you can feed the value directly into the tween like this:

```
gsap.to(CSSRulePlugin.getRule(".myClass::before"), {  
  duration: 3,  
  cssRule: { color: "#0000FF" },  
});
```