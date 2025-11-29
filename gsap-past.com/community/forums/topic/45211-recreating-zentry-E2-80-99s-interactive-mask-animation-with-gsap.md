---
source_url: "https://gsap.com/community/forums/topic/45211-recreating-zentry%E2%80%99s-interactive-mask-animation-with-gsap/"
title: "Recreating Zentry’s Interactive Mask Animation with GSAP - Banner Animation - GreenSock"
crawl_date: "2025-11-29T16:48:00.039672Z"
selector: "article"
---

# Recreating Zentry’s Interactive Mask Animation with GSAP - Banner Animation - GreenSock

![JecyNside](data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%201024%201024%22%20style%3D%22background%3A%2362c485%22%3E%3Cg%3E%3Ctext%20text-anchor%3D%22middle%22%20dy%3D%22.35em%22%20x%3D%22512%22%20y%3D%22512%22%20fill%3D%22%23ffffff%22%20font-size%3D%22700%22%20font-family%3D%22-apple-system%2C%20BlinkMacSystemFont%2C%20Roboto%2C%20Helvetica%2C%20Arial%2C%20sans-serif%22%3EJ%3C%2Ftext%3E%3C%2Fg%3E%3C%2Fsvg%3E)

### JecyNside

[Posted November 22](https://gsap.com/community/forums/topic/45211-recreating-zentry%E2%80%99s-interactive-mask-animation-with-gsap/?do=findComment&comment=220917)

Posted November 22

I'm trying to recreate the animation from **zentry.com**, specifically the effect where an **SVG clipPath deforms dynamically with the mouse movement**. I already have GSAP working for rotations and 3D interactions, but I can’t find a clear way to **animate the clipPath by updating the path’s coordinates (M, L, Q, etc.) in real time**.

What I need is guidance on how to **rebuild and replace the SVG path points using GSAP’s `attr: { d: "" }`** to achieve that smooth, responsive deformation like Zentry’s effect. Any examples or references would be greatly appreciated.