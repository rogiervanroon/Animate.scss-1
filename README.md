# Animate.scss

The Sassy version of the much loved [Animate.css](https://github.com/daneden/animate.css). Why? Because I wanted a way to drop in the entire collection without bloat & without the hassle of cherry-picking per project. 

## Get Started

1. Add the `animate` folder to your Sass source directory. 
2. Add `@import "animate/import";` to your Sass flow. 
3. Edit `_animate.scss`. Set `true` to include an animation. Set `false` to exclude.
4. Animate!

## @include

`$delay` = false || 300ms

`$infinite` = false || true

      @include animated($duration: 300ms, $delay: false, $infinite: false) 

## @extend

    @extend %bounce;
    @extend %bounceIn;
    @extend %bounceInDown;
    @extend %bounceInLeft;
    @extend %bounceInRight;
    @extend %bounceInUp;

    @extend %bounceOut;
    @extend %bounceOutDown;
    @extend %bounceOutLeft;
    @extend %bounceOutRight;
    @extend %bounceOutUp;

    @extend %fadeIn;
    @extend %fadeInDown;
    @extend %fadeInDownBig;
    @extend %fadeInLeft;
    @extend %fadeInLeftBig;
    @extend %fadeInRight;
    @extend %fadeInRightBig;
    @extend %fadeInUp;
    @extend %fadeInUpBig;

    @extend %fadeOut;
    @extend %fadeOutDown;
    @extend %fadeOutDownBig;
    @extend %fadeOutLeft;
    @extend %fadeOutLeftBig;
    @extend %fadeOutRight;
    @extend %fadeOutRightBig;
    @extend %fadeOutUp;
    @extend %fadeOutUpBig;

    @extend %flash;

    @extend %flipInX;
    @extend %flipInY;
    @extend %flipOutX;
    @extend %flipOutY;

    @extend %headShake;
    @extend %heartBeat;
    @extend %hinge;
    @extend %jackInTheBox;
    @extend %jello;

    @extend %lightSpeedIn;
    @extend %lightSpeedOut;

    @extend %pulse;

    @extend %rollIn;
    @extend %rollOut;

    @extend %rotateIn;
    @extend %rotateInDownLeft;
    @extend %rotateInDownRight;
    @extend %rotateInUpLeft;
    @extend %rotateInUpRight;

    @extend %rotateOut;
    @extend %rotateOutDownLeft;
    @extend %rotateOutDownRight;
    @extend %rotateOutUpLeft;
    @extend %rotateOutUpRight;

    @extend %rubberBand;

    @extend %scaleInDown;
    @extend %scaleOutUp;  
    
    @extend %shake;

    @extend %slideInDown;
    @extend %slideInLeft;
    @extend %slideInRight;
    @extend %slideInUp;

    @extend %slideOutDown;
    @extend %slideOutLeft;
    @extend %slideOutRight;
    @extend %slideOutUp;

    @extend %swing;
    @extend %tada;
    @extend %wobble;

    @extend %zoomIn;
    @extend %zoomInDown;
    @extend %zoomInLeft;
    @extend %zoomInRight;
    @extend %zoomInUp;

    @extend %zoomOut;
    @extend %zoomOutDown;
    @extend %zoomOutLeft;
    @extend %zoomOutRight;
    @extend %zoomOutUp;

## Basic Mobile Menu

Let's say we want to animate the following mobile menu:

- `#mobile-overlay` should fade in and out. 
- `#mobile-content` should slide open and closed from the right. 
- `#mobile-top` and `#mobile-bottom` should fade in. These do not need an out transition. 
- `mobile-menu` should fade in from the right. This does not need an out transition. 
- Durations and delays should create a subtle, layered effect.
- To help create the layered effect, the open animations can use up to 500ms. 
- The close animation does take 500ms, but is visually a bit faster. 

```
<nav id="mobile-nav" aria-label="Site Navigation"> 

      <button id="mobile-open">+</button>

      <div id="mobile-overlay">

            <button id="mobile-close">X</button>

            <div id="mobile-content">

                  <div id="mobile-top"></div>

                  <ul id="mobile-menu" class="menu"></ul>

                  <div id="mobile-bottom"></div>

            </div><!-- #mobile-content -->

      </div><!-- #mobile-overlay -->

</nav><!-- #mobile-nav -->
```

## The Premise

We're going to use vanila JavaScript  to add and remove a `[data-mobile]` attribute to the elments we're animating. This gives each elment several CSS states to work with:

```
#element {}

#element:not([data-mobile]) {}

#element[data-mobile] {}

#element[data-mobile="true"] {}

#element[data-mobile="false"] {}

```

## #mobile-overlay CSS

- Needs to start and end with `display: none` so the contents are hidden to keyboard navigation. 
- Should be the first thing to fade in - the animation should be the first and relatively fast. 
- Should be the last thing to fade out - the animation should be the longest or delayed. I went with longer.

```
// Styles that don't affect the transition can go here.
#mobile-overlay {}

// By setting the display here,
// we don't need JS to set inline CSS. 
#mobile-overlay:not([data-mobile]) {
    display: none;
}

// If the open and close timing were the same,
// we could put @include animated here. 
#mobile-overlay[data-mobile] {
   // nothing here
}

// Open
#mobile-overlay[data-mobile="true"] {
      @include animated(300ms);
      @extend %fadeIn;
}

// Close
// This is the longest close animation - important
// to the JS timeout on the mobileSweep function. 
#mobile-overlay[data-mobile="false"] {
      @include animated(500ms);
      @extend %fadeOut;
}
```

## #mobile-content CSS

- This is the main mobile menu container. 
- It should slide in and out from the right.
- On open, it should wait a bit to let the overlay start.
- On close, it should finish exiting just ahead of the overlay fading out. 
    
```
// Open
#mobile-content[data-mobile="true"] {
    @include animated(300ms, 100ms); // wait for overlay
    @extend %slideInRight;
}

// Close
#mobile-content[data-mobile="false"] {
    @include animated(300ms);
    @extend %slideOutRight;
}
```

## #mobile-top & #mobile-bottom CSS

- These are blocks above and below the menu's `ul` block. Things like branding, social links, and search forms would go in these. 
- These should fade in as the menu opens. 
- The fade should wait a bit for `#mobile-content`, which has a delay. 
- These do not need a close animation. 

```
// Open
#mobile-top[data-mobile="true"],
#mobile-bottom[data-mobile="true"] {
    @include animated(300ms, 200ms); // wait for overlay + content
    @extend %fadeIn;
}
```

## #mobile-menu CSS

- This is the main `ul` block. 
- It should fade in from the right. 
- The fade should wait a bit for `#mobile-content`, which has a delay.
- This does not need a close animation. 

```
// Open
#mobile-menu[data-mobile="true"] {
    @include animated(200ms, 300ms); // wait for overlay + content
    @extend %fadeInRight;
}
```

## Basic JS

The JavaScript for animating will use 3 handlers:

```
// Animation Elements
let mobile_overlay = document.getElementById('mobile-overlay');
let mobile_content = document.getElementById('mobile-content');
let mobile_top = document.getElementById('mobile-top');
let mobile_menu = document.getElementById('mobile-menu');
let mobile_bottom = document.getElementById('mobile-bottom');


// Open animation
function mobileOpenAnimate() {
      document.body.setAttribute('data-mobile', 'true');
      mobile_overlay.setAttribute('data-mobile', 'true');
      mobile_content.setAttribute('data-mobile', 'true');
      mobile_top.setAttribute('data-mobile', 'true');
      mobile_menu.setAttribute('data-mobile', 'true');
      mobile_bottom.setAttribute('data-mobile', 'true');
} //

// Close animation
function mobileCloseAnimate() {
      mobile_overlay.setAttribute('data-mobile', 'false');
      mobile_content.setAttribute('data-mobile', 'false');

      // Not animated out - removed on sweep
      // mobile_top.setAttribute('data-mobile', 'false');   
      // mobile_menu.setAttribute('data-mobile', 'false');   
      // mobile_bottom.setAttribute('data-mobile', 'false');   
} //

// Sweep
// Most important for returning the overlay to display: none. 
function mobileSweep() {
      var sweep_mobile = Array.from(document.querySelectorAll('[data-mobile]'));
      sweep_mobile.forEach(element => {
            element.removeAttribute('data-mobile');
      });
} //
```

The Javascript click handlers need to include this:

```
function mobileOpenClick() {
      event.preventDefault();
      mobileOpenAnimate();
      // other stuff
} //

function mobileCloseClick() {
      event.preventDefault();
      mobileCloseAnimate();
      // other stuff
      
      // wait for longest close animation,
      // which is 500ms on the overlay
      setTimeout(() => {
            mobileSweep();
      }, 501); 
} //

