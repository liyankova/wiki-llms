---
source_url: "https://gsap.com/core/"
title: "Core | GSAP"
crawl_date: "2025-11-29T16:37:36.662347Z"
selector: "main"
---

# Core | GSAP

# Core

### 

One library, unlimited inspiration

## GSAP Core - everything you need to create blazingly fast, responsive animations for all browsers.

* [Docs](/docs/v3)
* [Showcase](/showcase/)

## Animate Anything

GSAP is framework agnostic and endlessly flexible - animate any property of any object with a simple Tween.

* CSS
* React
* SVG
* WebGL

* ```
  <div id="animate-anything-css"></div>  
    
  gsap.to("#animate-anything-css", {  
    duration: 10,  
    ease: "none",  
    repeat: -1,  
    rotation: 360,  
  })
  ```
* ```
  const RotatingCube = () => {  
    const boxRef = useRef()  
    
    useGSAP(() => {  
      gsap.to(boxRef.current, {  
        duration: 10,  
        repeat: -1,  
        rotation: 360,  
      })  
    })  
    
    return (  
      <div ref={boxRef} />  
    )  
  }
  ```
* ```
  <svg>  
    <g id="animate-anything-svg">  
      ...  
    </g>  
  </svg>  
    
  gsap.to("#animate-anything-svg", {  
    duration: 10,  
    ease: "none",  
    repeat: -1,  
    rotation: 360,  
  })
  ```
* ```
  const cube = new Mesh(geometry, material)  
  scene.add(cube)  
    
  gsap.to(cube.rotation, {  
    x: Math.PI * 2,  
    y: Math.PI * 2,  
    duration: 10,  
    repeat: -1,  
    ease: "none",  
    onUpdate: () => {  
      renderer.render(scene, camera)  
    },  
  })
  ```

## GSAP Timeline, The Ultimate Sequencing Tool

Arrange Tweens in a Timeline to precisely choreograph animations. Control entire sequences as a whole using methods like play(), pause(), reverse(), timeScale() and seek()

```
const tl = gsap.timeline({paused: true});  
  
tl.to(".scrubber", { x: 500, duration: 2 })  
	.to(".mask",{ scaleX: 0},"<")  
	.to(".icon1",{scale: 1, duration: 0.3}, 0.5)  
	.to(".text1",{ autoAlpha: 1, scale: 1}, "-=0.2")  
  
	.add(sequence2,"+=0.1").timeScale(0.8)  
	  
	...  
  
	tl.seek(1.2).play()
```

## Responsive & Accessibility-Friendly

Set up animations for different viewport sizes and make then a11y friendly with gsap.matchMedia.

Reduced Motion

```
let mm = gsap.matchMedia();  
  
mm.add({  
 reduceMotion: "(prefers-reduced-motion: reduce)"  
}, (context) => {  
  
  let {reduceMotion} = context.conditions;  
  
  gsap.to(".windmill", {  
		rotation: 360,  
    // adjust animation in tweens  
		duration: reduceMotion ? 7.2 : 3.6,  
	});  
  
  // or set up easy conditionals  
  if (!reduceMotion) {   
   let tl = gsap.timeline()  
   tl.to()...  
  }  
});
```

## Extend the Core with GSAP's Plugins

* ### 

  Flip

  ### Seamlessly transition between two state. Flip does the heavy lifting.

  [Flip](/docs/v3/Plugins/Flip/)
* ### 

  ScrollTrigger

  ### Jaw-dropping scroll-based animations with minimal code.

  [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* ### 

  MotionPath

  ### Forge your own (motion) path with this powerful plugin.

  [MotionPath](/docs/v3/Plugins/MotionPathPlugin/)
* ### 

  Draggable

  ### Make virtually any DOM element draggable, spinnable, and more.

  [Draggable](/docs/v3/Plugins/Draggable/)
* ### 

  Observer

  ### Tell Observer which event types to watch and it will collect delta values.

  [Observer](/docs/v3/Plugins/Observer/)

* [Get

  GSAP](/docs/v3/Installation)

## Need answers?

### Connect the Dots

Head over to the GSAP Community Forum to ask questions, find answers and connect with other users.

[Visit Community](/community)

### 

Featured Community Demos

* [

  ](https://gsap.com/community/uploads/monthly_2025_02/core-sine.mp4.fe2e09d1ada0165e3be1ded36f651f8a.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/core-sine.jpeg.712e72021ae7ffe3d98e4464441c5771.jpeg)

  [### Sine Wave](https://codepen.io/osublake/pen/ExPMgQq)

  ### 

  Blake Bowen
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/core-pixelated.mp4.dfc04715118aba8070168da3bcb02ce3.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/core-pixelated.jpeg.86e3e21f875e28f16394c531911d8d0b.jpeg)

  [### Pixelated Image Reveal](https://codepen.io/osmosupply/pen/OJKjWNz)

  ### 

  Osmo
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/core-particles.mp4.1ac16a8df8cce3e74e834879a13770a3.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/core-particles.jpeg.8abd73626ad0f34c7bf3eb15820ac6ea.jpeg)

  [### canvas particles](https://codepen.io/GreenSock/pen/NWZRRNb)

  ### 

  Tom Miller
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/core-torus.mp4.df1dd8ff9d770d4bbc07186c7248910b.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/core-torus.jpeg.af243bc12dc16f5dbbe87e62863a318f.jpeg)

  [### Torus Loader](https://codepen.io/kdbkapsere/pen/LYZrxEp)

  ### 

  Kasper De Bruyne
* [

  ](https://gsap.com/community/uploads/monthly_2025_02/core-rube.mp4.b6dc8c007422e5e9ee2733dc9e353607.mp4)

  ![](https://gsap.com/community/uploads/monthly_2025_02/core-rube.jpeg.7671ca3215e815f95e66c9686b7be6c0.jpeg)

  [### Rube Goldberg HTML form](https://codepen.io/ksenia-k/pen/xxoqXbJ)

  ### 

  Ksenia Kondrashova

[Demos on Codepen](https://codepen.io/collection/mreqar)

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