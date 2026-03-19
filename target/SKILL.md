---
name: gsap-cheat-sheet-skills
description: Quick reference of commonly used GSAP APIs and patterns extracted from the GSAP Cheat Sheet page.[page:1]
---

here are the instructions for Gsap animations -use them when building websites or apps


## Basics

### Core tweens

```js
// "to" tween - animate to provided values
gsap.to(".selector", {
  // selector text, Array, or object
  x: 100,                     // any properties (not limited to CSS)
  backgroundColor: "red",     // camelCase
  duration: 1,                // seconds
  delay: 0.5,                 // seconds
  ease: "power2.inOut",
  stagger: 0.1,               // stagger start times
  paused: true,               // default is false
  overwrite: "auto",          // default is false
  repeat: 2,                  // -1 for infinite
  repeatDelay: 1,             // seconds between repeats
  repeatRefresh: true,        // invalidates on each repeat
  yoyo: true,                 // if true: A-B-B-A, if false: A-B-A-B
  yoyoEase: true,             // or ease like "power2"
  immediateRender: false,
  onComplete: () => {
    console.log("finished");
  }
  // other callbacks: onStart, onUpdate, onRepeat, onReverseComplete
});
```

```js
// "from" tween - animate from provided values
gsap.from(".selector", {
  // fromVars
});
```

```js
// "fromTo" tween - define both start and end values
gsap.fromTo(
  ".selector",
  { /* fromVars */ },
  { /* toVars, including duration/ease/etc. */ }
);
```

```js
// Set values immediately (no animation)
gsap.set(".selector", {
  // toVars
});
```

---

## Timelines

### Creating timelines

```js
// Create a timeline
let tl = gsap.timeline({
  delay: 0.5,
  paused: true,          // default is false
  repeat: 2,             // -1 for infinite
  repeatDelay: 1,        // seconds between repeats
  repeatRefresh: true,   // invalidates on each repeat
  yoyo: true,            // if true: A-B-B-A
  defaults: {            // children inherit these defaults
    duration: 1,
    ease: "none"
  },
  smoothChildTiming: true,
  autoRemoveChildren: true,
  onComplete: () => {
    console.log("finished");
  }
  // other callbacks: onStart, onUpdate, onRepeat, onReverseComplete
});
```

### Sequencing tweens

```js
// Sequence multiple tweens
tl.to(".selector", {
  duration: 1,
  x: 50,
  y: 0
})
  .to("#id", {
    autoAlpha: 0
  })
  .to(elem, {
    duration: 1,
    backgroundColor: "red"
  })
  .to([elem, elem2], {
    duration: 3,
    x: 100
  });
```

### Position parameter

```js
tl.to(target, { /* toVars */ }, positionParameter);

// Examples:
0.7;           // exactly 0.7 seconds into the timeline (absolute)
"-=0.7";       // overlap with previous by 0.7 sec
"myLabel";     // insert at "myLabel" position
"myLabel+=0.2"; // 0.2 seconds after "myLabel"
"<";           // align with start of most recently-added child
"<0.2";        // 0.2 seconds after ^
"-=50%";       // overlap half of inserting animation's duration
"<25%";        // 25% into the previous animation (from its start)
```

---

## Control Methods

### Tween / timeline control

```js
// Retain animation reference to control later
let anim = gsap.to(".selector", { x: 100 });
// or: let anim = gsap.timeline({...});

// Most methods can be used as getters or setters
anim
  .play()            // plays forward
  .pause()
  .resume()          // respects direction
  .reverse()
  .restart()
  .timeScale(2)      // 2 = double speed, 0.5 = half speed
  .seek(1.5)         // jump to a time (in seconds) or label
  .progress(0.5)     // jump to halfway
  .totalProgress(0.8) // includes repeats

  // Other useful methods (tween and timeline)
  .kill()            // immediately destroy
  .isActive()        // true if currently animating
  .then(() => {})    // Promise
  .invalidate()      // clear recorded start/end values
  .eventCallback("onComplete", () => {}); // get/set event callbacks
```

### Timeline-specific helpers

```js
anim
  .add(thing, position)      // add label, tween, timeline, or callback
  .call(func, params, position) // calls function at given point
  .getChildren()             // get an Array of the timeline's children
  .clear()                   // empties the timeline
  .tweenTo(timeOrLabel, { vars }) // animate playhead linearly to position
  .tweenFromTo(from, to, { vars }); // same but with start and end
```

---

## Eases

```js
// Basic core eases
ease: "none"; // same as "linear"

"power1", "power2", "power3", "power4", "circ", "expo", "sine";
// each has .in, .out, and .inOut extensions, e.g. "power1.inOut"

// Expressive core eases
"elastic", "back", "bounce", "steps(n)";

// In EasePack plugin (not core)
"rough", "slow", "expoScale(1, 2)";

// Expressive plugin eases
// CustomEase, CustomWiggle, CustomBounce (via corresponding plugins)
```

---

## ScrollTrigger

```js
gsap.to(".selector", {
  scrollTrigger: {
    trigger: ".selector",        // selector or element
    start: "top center",         // [trigger] [scroller] positions
    end: "20px 80%",             // positions or relative amount: "+=500"
    scrub: true,                 // or time (in seconds) to catch up
    pin: true,                   // or selector/element to pin
    markers: true,               // only during development!
    toggleActions: "play pause resume reset",
    // other actions: complete reverse none
    toggleClass: "active",
    fastScrollEnd: true,         // or velocity number
    containerAnimation: tween,   // linear animation
    id: "my-id",
    anticipatePin: 1,            // may help avoid jump
    snap: {
      snapTo: 1 / 10,            // progress increment or "labels"/fn/Array
      duration: 0.5,
      directional: true,
      ease: "power3",
      onComplete: callback       // onStart, onInterrupt also available
    },
    pinReparent: true,           // moves to documentElement during pin
    pinSpacing: false,
    pinType: "transform",        // or "fixed"
    pinnedContainer: ".selector",
    preventOverlaps: true,       // or arbitrary string
    once: true,
    endTrigger: ".selector",     // selector or element
    horizontal: true,            // switches mode
    invalidateOnRefresh: true,   // clears start values on refresh
    refreshPriority: 1,          // influence refresh order
    onEnter: callback
    // other callbacks:
    // onLeave, onEnterBack, onLeaveBack, onUpdate,
    // onToggle, onRefresh, onRefreshInit, onScrubComplete
  }
});
```

---

## Plugins

### Registering plugins

```js
// Register GSAP plugins (once) before using them
gsap.registerPlugin(Draggable, TextPlugin);
```

### Available plugins (by category)

- General: Draggable, GSDevTools, Observer, InertiaPlugin.[page:1]
- SVG: DrawSVGPlugin, MorphSVGPlugin, MotionPathPlugin, MotionPathHelper.[page:1]
- Scroll: ScrollTrigger, ScrollSmoother, ScrollToPlugin.[page:1]
- Text: SplitText, ScrambleTextPlugin, TextPlugin.[page:1]
- Other: Physics2DPlugin, PhysicsPropsPlugin, PixiPlugin, Flip.[page:1]

---

## Installation

```js
// Import and register GSAP
import { gsap } from "gsap";
import { DrawSVGPlugin } from "gsap/DrawSVGPlugin";

gsap.registerPlugin(DrawSVGPlugin);
```

---

## Utility Methods

```js
// accessible through gsap.utils.foo()
gsap.utils.checkPrefix(prop);   // get relevant browser prefix for property
gsap.utils.clamp(min, max);     // clamp value to range
gsap.utils.distribute(config);  // distribute value among an array
gsap.utils.getUnit(str);        // get unit of string
gsap.utils.interpolate(a, b);   // interpolate between values
gsap.utils.mapRange(a1, a2, b1, b2); // map one range to another
gsap.utils.normalize(min, max); // map a range to the 0–1 range
gsap.utils.pipe(fn1, fn2);      // sequence function calls
gsap.utils.random(min, max, snapIncrement, [seed]);
gsap.utils.selector(scope);     // scoped selector function
gsap.utils.shuffle(array);      // shuffles an array in-place
gsap.utils.snap(incrementOrArray); // snap to increment or array
gsap.utils.splitColor(color);   // splits color into RGB array
gsap.utils.toArray(targets);    // convert array-like to array
gsap.utils.unitize(fn, unit);   // adds unit to function results
gsap.utils.wrap(min, max);      // wrap number in range
gsap.utils.wrapYoyo(min, max);  // wrap in range, reversing on wrap
```

---

## Nesting Timelines

```js
function scene1() {
  let tl = gsap.timeline();
  tl.to(".box1", { x: 100 }).to(".box1", { y: 50 }); // build scene 1
  return tl;
}

function scene2() {
  let tl = gsap.timeline();
  tl.to(".box2", { x: 200 }).to(".box2", { rotation: 45 }); // build scene 2
  return tl;
}

let master = gsap.timeline()
  .add(scene1())
  .add(scene2(), "-=0.5"); // overlap slightly
```

---

## Miscellaneous

```js
// Get the current value of a property
gsap.getProperty("#id", "x");        // 20
gsap.getProperty("#id", "x", "px");  // "20px"
```

```js
// Set GSAP's global tween defaults
gsap.defaults({
  ease: "power2.in",
  duration: 1
});
```

```js
// Configure GSAP's non-tween-related settings
gsap.config({
  autoSleep: 60,
  force3D: false,
  nullTargetWarn: false,
  trialWarn: false,
  units: {
    left: "%",
    top: "%",
    rotation: "rad"
  }
});
```

### Effects API

```js
// Register an effect for reuse
gsap.registerEffect({
  name: "fade",
  effect: (targets, config) => {
    return gsap.to(targets, {
      duration: config.duration,
      opacity: 0
    });
  },
  defaults: { duration: 2 },
  extendTimeline: true
});

// Use effect
gsap.effects.fade(".box");

// Or directly on timelines
tl.fade(".box", { duration: 3 });
```

### Ticker

```js
// Add listener with gsap.ticker
gsap.ticker.add(myFunction);

function myFunction(time, deltaTime, frame) {
  // Executes on every tick after the core engine updates
}

// Remove the listener later
gsap.ticker.remove(myFunction);
```

### quickSetter / quickTo

```js
// Faster way to repeatedly set property than .set()
let setX = gsap.quickSetter("#id", "x", "px");

document.addEventListener("mousemove", e => setX(e.clientX));

// quickTo - for animation based on updates
let xTo = gsap.quickTo("#id", "x", {
  duration: 0.4,
  ease: "power3"
});

document.addEventListener("mousemove", e => xTo(e.pageX));
```
```