---
source_url: "https://gsap.com/scroll/"
title: "Scroll | GSAP"
crawl_date: "2025-11-29T16:37:40.151844Z"
selector: "main"
---

# Scroll | GSAP

# Scroll

![](/tf-assets/scroll-tube-cbe21ede.png)

![](/tf-assets/scroll-tube-2-682ae4e4.png)

![](/tf-assets/scroll-tube-cbe21ede.png)

### 

GSAP allows you to create jaw dropping scroll effects with minimal code for maximum impact.

## Scroll Plugins

Infinitely Flexible,  
Highly Optimised

Debounced events, pre-calculated intersection points, synced updates and throttled resize recalculations. We tackle performance headaches so you can focus on the fun stuff.

![](/tf-assets/full-5246906a.png)

Slide, zoom, morph, draw. Link any GSAP animation to scroll - it’s completely framework agnostic.

![](/tf-assets/worm-d995fc59.png)

## ScrollTrigger

Ready, Set,  
Scroll

Tell stunning and interactive stories. Give any tween or timeline a ScrollTrigger with just one line of code or customise as needed.

```
gsap.timeline({  
  scrollTrigger: {  
    scrub: 1,  
    trigger: ".scroll-trigger-ready__worm-wrap",  
    start: "top 90%",  
    end: "bottom 30%",  
  },  
});
```

[Demos](https://codepen.io/collection/DkvGzg)
[Docs](/docs/v3/Plugins/ScrollTrigger)

Start

End

## Pin, Scrub, Debug

Pin sections in place, scrub through animations with the scrollbar, and debug easily by enabling visual markers.

```
const tl = gsap.timeline({  
  scrollTrigger: {  
    scrub: 1,  
    pin: true,  
    trigger: "#pin-windmill",  
    start: "50% 50%",  
    endTrigger: "#pin-windmill-wrap",  
    end: "bottom 50%",  
  },  
});  
  
tl.to("#pin-windmill-svg", {  
  rotateZ: 900,  
});
```

Craft animations for any viewport size with gsap.matchMedia()

## ScrollSmoother

It’s like a gentle breeze

Effortlessly guiding your users from one section to another.

![](/tf-assets/worm-2-afec0379.png)

## It’s smooth like butter

ScrollSmoother leverages the native scroll mechanics meaning you can deliver a fluid and immersive experience for everyone, no matter the device or user input.

[Demos](https://codepen.io/collection/BNMEYN)
[Docs](/docs/v3/Plugins/ScrollSmoother)

![](/tf-assets/spiral-1-9bfa045a.png)

![](/tf-assets/spiral-2-fb7f885f.png)

![](/tf-assets/spiral-3-8cd34159.png)

![](/tf-assets/spiral-4-9810c545.png)

![](/tf-assets/spiral-5-f06ea89c.png)

![](/tf-assets/spiral-6-e7bcdc8d.png)

![](/tf-assets/spiral-7-323adaf0.png)

## Create mesmerising effects

Add gorgeous parallax and trailing effects by simply adding a data attribute

```
<div data-speed="0.8"></div>  
<div data-speed="2.0"></div>  
<div data-speed="1.2"></div>
```

## Seamlessly integrated

Get all the capabilities of GSAP and ScrollTrigger with the added benefits of smooth scrolling. With tight integration across the whole ecosystem, even the most complex animations look flawless.

## Back to Basics with Observer

Need more low-level control? Easily detect scroll and other events without wrestling with implementation details.

[Demos](https://codepen.io/collection/KpNYOd)
[Docs](/docs/v3/Plugins/Observer)

## Buttery Smooth Scrolling With GSAP Scroll Plugins

* ### 

  ScrollSmoother

  ### The easiest way to make buttery smooth work of scrolling.

  [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* ### 

  ScrollTrigger

  ### Jaw-dropping scroll-based animations with minimal code.

  [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* ### 

  ScrollTo

  ### Take your users on a wild scroll ride to wherever they need to go.

  [ScrollTo](/docs/v3/Plugins/ScrollToPlugin/)
* ### 

  Observer

  ### Tell Observer which event types to watch and it will collect delta values.

  [Observer](/docs/v3/Plugins/Observer)

* [Get

  GSAP](/docs/v3/Installation)

### 

Featured Community Demos

* [

  ](https://gsap.com/community/uploads/monthly_2025_02/blackbird.mp4.4d47bc4e355e75d388b1a95cfbd08710.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/blackbird.jpeg.f0eb542a1e330eb78869d9e8328766f1.jpeg)

  [### GSAP ScrollSmoother + Three.js](https://codepen.io/cmalven/pen/PoEJvjE)

  ### 

  Malven
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/plane.mp4.d63dc1d8f8b9caa2d96f4bb78e41e001.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/plane.jpeg.fb789a7b586c1169213ddfaa9b8cb0fe.jpeg)

  [### Airplanes.](https://codepen.io/ste-vg/pen/GRooLza)

  ### 

  Steve Gardner
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/goo.mp4.fd85b7ad3317994dc820ac568772bf39.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/goo.jpeg.3ba6c6c3633204a6f188a67489497639.jpeg)

  [### On-Scroll Gooey Overlay](https://codepen.io/ksenia-k/pen/NWmMxLg)

  ### 

  Ksenia Kondrashova
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/disintegration.mp4.1e4373b8dbfde39ffa0f27753ded85ef.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/disintegration.jpeg.44ad2a217eaf184626e88f9bc9407c9f.jpeg)

  [### Disintegration Effect](https://codepen.io/dev_loop/pen/mdVWRMv)

  ### 

  Sikriti Dakua
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/infinite.mp4.7df30143c33cd205b84a80511e0eb5b1.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/infinite.jpeg.97f42725b8df3b59984bfd97bec2bcd0.jpeg)

  [### Infinite Cover Flow](https://codepen.io/jh3y/pen/WNRvqJP)

  ### 

  Jhey
* [

  ](https://gsap.com/community/uploads/monthly_2025_04/eric.mp4.60ed32bbe49d0a297a98e1077f163a21.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_04/eric.jpg.ee3ae8f90e16328c3578acade464a4d2.jpg)

  [### Poster Randomizer](https://codepen.io/vanholtzco/full/VYwRdob/d509fa0b3dfabb3a069fd97d36e4c17c)

  ### 

  Eric Van Holtz
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/tube.mp4.84683cba88b202c14597de417cb3c384.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/tube.jpeg.7b21809e4c0f450c3b0ee00b735226a3.jpeg)

  [### Scroll Through WebGL Tunnel/Tube](https://codepen.io/motionharvest/pen/WNQYJyM)

  ### 

  Motion Harvest
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/fishes.mp4.5b1229c806d7dc5bbce73226bde027b2.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/fishes.jpeg.0d27f0458f66c751981c02f3298542a6.jpeg)

  [### Weird Fishes](https://codepen.io/michellebarker/pen/dyMQYYz)

  ### 

  Michelle Barker

[Demos on Codepen](https://codepen.io/collection/bNPYOw)

### Showcase

[](https://gsap.com/community/uploads/monthly_2025_01/trimmed.mp4.b3ee24a03e178b0c306dba74ff29e698.mp4)

[](https://gsap.com/community/uploads/monthly_2025_09/09-17-2025-won-j-you-video-sow.mp4.3dd45d0fff243ac7687cabaeeb2709ba.mp4)

[](https://gsap.com/community/uploads/monthly_2025_09/09-10-2025-martin-laxenaire-video.mp4.a79aa5593619cec7ecc0508dbf499b30.mp4)

[](https://gsap.com/community/uploads/monthly_2025_09/09-03-2025-tubik-video.mp4.61a08ba32351b33e443069067b8a13f2.mp4)

[](https://gsap.com/community/uploads/monthly_2025_08/ABOUTMarkWoodlandUncommonStudioMelbourne-08-27-2025.mp4.872bdf7fa2123d68cc89746b09b356b7.mp4)

[](https://gsap.com/community/uploads/monthly_2025_08/GSAP_screen_sm.mp4.c25d420179223c1060991bdf5a229f77.mp4)

[GSAP Showreel 2024](https://www.youtube.com/watch?v=ic-bHSoIUaA)

[Won J. You
 /](https://wonjyou.studio/)

ScrollTrigger, Flip, SplitText

[Explore All Showcases](/showcases)