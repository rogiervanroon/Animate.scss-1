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
    On open, this should wait a bit for `#mobile-overlay` to start.
    On close, this should finish exiting a bit faster than `#mobile-overlay`. 
- `#mobile-top` and `#mobile-bottom` should fade in. These do not need an out transition. 
- `mobile-menu` should fade in from the right. This does not need an out transition. 

```
<nav id="mobile-nav" aria-label="Site Navigation"> 

      <button id="mobile-open">
      <i class="fas fa-bars"></i>
      </button>

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

## The Overlay

- Needs to start and end with `display: none` so the contents are hidden to keyboard navigation. 
- Should be the first thing to fade in. 
- Should be the last thing to fade out. 

*CSS*

```
// On load + after close 
#mobile-overlay:not([data-mobile]) {
    display: none;
}

// The overlay can fade in and out at same rate,
// so we put the animating timing here. 
#mobile-overlay[data-mobile] {
    @include animated(800ms);
}

// Open
#mobile-overlay[data-mobile="true"] {
    @extend %fadeIn;
}

// Close
#mobile-overlay[data-mobile="false"] {
    @extend %fadeOut;
}
```

*JS*

```
// todo
```

## Basic JS
    
```
// todo
```

