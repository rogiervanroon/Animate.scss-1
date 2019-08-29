# Animate.scss

The Sassy version of the much loved [Animate.css](https://github.com/daneden/animate.css). Why? Because I wanted a way to drop in the entire collection without bloat & without the hassle of cherry-picking per project. 

## Get Started

1. Add the `animate` folder to your Sass source directory. 
2. Add `@import "animate/import";` to your Sass flow. 
3. Edit `_animate.scss` to include / exclude animations. 
4. Animate!

## Basic HTML

    <div id="modal">
        <button id="modal-open"></button>
        <div id="modal-overlay">
            <button id="modal-close"></button>
            <div id="modal-content">
                <!-- content her -->
            </div><!-- #modal-content -->
        </div><!-- #modal-overlay -->
    </div><!-- #modal -->

## Bascic CSS

Using `data-modal` attribute set via JavaScript

    // Either fallback styles (na here)
    // or styles that don't impact tranition
    #modal-content {}

    // The initial state
    #modal-content:not([data-modal]) {}

    // Transition timing + delay
    #modal-content[data-modal] {
        @include animated(500ms);
    }

    // Open transition
    #modal-content[data-modal="true"] {
        @extend %bounceInLeft;
    }

    // Close transition
    #modal-content[data-modal="false"] {
        @extend %bounceOutRight;
    }

## Basic JS
    
    // todo

## @include

    @include animated($duration, $delay);
    @include animated-infinite; 

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

