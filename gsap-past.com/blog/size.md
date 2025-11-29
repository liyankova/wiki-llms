---
source_url: "https://gsap.com/blog/size"
title: "Rethinking Kilobytes | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:21:29.899475Z"
selector: "article"
---

# Rethinking Kilobytes | GSAP | Docs & Learning

Conventional wisdom says that kilobytes have a direct impact on load times and consequently user experience. Too many developers, however, myopically focus on a simplistic (and rather dated) "aggregate total file size" mentality and completely miss the broader goal of improving user experience. This article aims to challenge the old paradigm and explain why "spending" kilobytes on a library like GSAP can be a very smart move.

## Kilobyte cost factors[​](#kilobyte-cost-factors "Direct link to Kilobyte cost factors")

When you're assessing kilobyte cost in a modern, nuanced way consider these factors:

### Performance yield[​](#performance-yield "Direct link to Performance yield")

Would you spend an extra 200ms of load time to get super-smooth animations at runtime? Are users more sensitive to janky animations the whole time they're interacting with your site...or a fraction of a second on initial load? Of course there are reasonable limits either way (waiting an extra 30 seconds for a huge file to load would be intolerable even if it made things run buttery smooth), but in most cases we're only talking about fractions of a second difference. GSAP contains "extra" code that automatically GPU-accelerates transforms, applies lag smoothing, avoids layout thrashing, caches important values for super-fast lookups, etc. - would removing those features for the sake of a few milliseconds on initial load (and zero savings once it's cached) be a step forward or backward?

### Caching[​](#caching "Direct link to Caching")

When does a 23kb file act like a 0kb file? When it's cached! This is particularly relevant for engaging, animated sites because there are common tasks and code that can be encapsulated and shared. GSAP is a perfect example of a shared resource. An end user only loads it once and then it's completely "free" thereafter...for all pages pointing at that file...on all sites\*!

### Unique assets vs shared resources[​](#unique-assets-vs-shared-resources "Direct link to Unique assets vs shared resources")

\*Some browsers may implement domain-specific caching.

### CDN[​](#cdn "Direct link to CDN")

files loaded from a CDN (Content Delivery Network) are typically "faster" because they're geographically distributed and automatically loaded from the closest server. Plus CDNs have inherent redundancies leading to better reliability.

### Custom code reduction (kb savings)[​](#custom-code-reduction-kb-savings "Direct link to Custom code reduction (kb savings)")

Loading a library like GSAP may allow you to only write 1kb of custom animation code instead of 5kb of CSS animation code, for example. Plus it has quite a few utility methods that you can tap into for added savings. This can significantly reduce the amount of custom code that must be loaded as your visitors go page-to-page

## Non-kilobyte costs[​](#non-kilobyte-costs "Direct link to Non-kilobyte costs")

If you avoid a tried-and-true library like GSAP, it may feel like you're reducing your costs but don't forget:

### Development time[​](#development-time "Direct link to Development time")

You could use a minimalistic library or write your own, but how much more time will that take to implement? How much custom code will it require? How many workarounds will be required to get similar functionality? How many headaches will you run into with cross-browser quirks and inconsistencies that GSAP already solved? GSAP's API has been crafted over a decade to facilitate easy experimentation with minimal code. And when it comes to animation, experimentation is key. Most developers are working against deadlines and it's priceless to have a robust, vetted toolset to rely on.

### Swagger & confidence[​](#swagger--confidence "Direct link to Swagger & confidence")

Perhaps your project only has basic animation needs so you choose a basic animation library or write your own custom code for all the animations...but what happens when the client requests something more advanced? Uh oh. Will you port everything to GSAP then? What if you've got hundreds of animations that now need to be dynamically time-scaled or linked to scroll position with smooth scrubbing? How about advanced morphing, motion paths, and responsive animations? If you just use GSAP from the start, you have almost zero risk of running into an "oh no!" moment like that. You can code with confidence that you'll be able to animate pretty much anything with minimal code. What is that kind of developer swagger worth?

### Documentation, support & training[​](#documentation-support--training "Direct link to Documentation, support & training")

What if you run into trouble? Is excellent documentation available? Is there a community eager to help? Are there training resources for new hires down the road? What's the real long-term impact of your choice?

### Maintenance[​](#maintenance "Direct link to Maintenance")

The web is littered with abandoned open source projects. What's the track record of the one you're considering? How long has it been actively developed? Or if you're writing all your own animation code from scratch, is it truly maintainable? What's the long-term cost? Are you documenting how everything works? What happens when browsers introduce bugs or new features that impact animations?

### Other factors to consider[​](#other-factors-to-consider "Direct link to Other factors to consider")

Bandwidth is only increasing - The impact of a 24kb library is decreasing all the time. It's less than a single image these days. On average, in fact, images account for over 864kb on every web page! And again, GSAP is a one-time load in most cases. It's often cached in which case it costs nothing.

### GSAP doesn't count against file size budgets on every major ad network[​](#gsap-doesnt-count-against-file-size-budgets-on-every-major-ad-network "Direct link to GSAP doesn't count against file size budgets on every major ad network")

They have virtually all recognized GSAP as an industry standard and exempted it from file size calculations. That directly benefits you if your animations are GSAP-based. Google, Sizmek, Advertising.com, Flashtalking, AdWords, Flite, Cofactor, etc. - they're all on board with GSAP.

### Conclusion[​](#conclusion "Direct link to Conclusion")

The old mindset focused on the aggregate total file size for each page making it's easy to miscalculate the cost of using a library like GSAP (or any other shared resource). Doing so also pushes developers toward minimalistic less-capable solutions that may end up being far more expensive long-term. We'd encourage a more wholistic, nuanced approach that looks at the overall costs and benefits. Remember the end goals - outstanding user experience, minimal development costs, and long-term viability.