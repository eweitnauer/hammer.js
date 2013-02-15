# Hammer.js v2 (release candidate)  [![Build Status](https://travis-ci.org/EightMedia/hammer.js.png)](https://travis-ci.org/EightMedia/hammer.js/)

### A javascript library for multi-touch gestures

> I told you, homeboy /
> You *CAN* touch this /
> Yeah, that's how we living and you know /
> You *CAN* touch this

[![logo](https://www.paypalobjects.com/en_US/GB/i/btn/btn_donateCC_LG.gif)]
(https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=3E9CEAWH66M6J&lc=GB&item_name=Hammer%2ejs&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted)

## Demo
[Watch the demo's](http://eightmedia.github.com/hammer.js/v2/). 
It always needs some testing with all kind of devices, please contribute!


## Why the rewrite
- The previous Hammer.js became old, and too much of a hobby project: Inefficient code, bad documentation.
- It wasn't possible to add custom gestures, or change anything about the (inner) working of the gestures.
- It needed DOM events, to use with event delegation.
- Windows8 has touch AND mouse, so the Pointer Events API needs to be implemented.
- Did I mention the code was inefficient? Now a Hammer instance is light, and only contains the methods it should.


## Features in v2
- DOM Events
- Debug plugins
- Custom gestures api
- Better swipe event
- Chainable instance methods
- jQuery plugin with events delegation (the on/off methods) available
- Efficient code, lower memory usage
- IE8 and older compatibility with jQuery plugin
- More events for faster implementation
- AMD support (RequireJS)


## Getting Started
Hammer became simpler to use, with an jQuery-like API. You don't need to add the new keyword, and the eventlisteners are chainable.

````js
    var element = document.getElementById('test_el');
    var hammertime = Hammer(element).on("tap", function(event) {
        alert('hello!');
    });
````

You can change the default settings by adding an second argument with options

````js
    var hammertime = Hammer(element, {
        drag: false,
        transform: false
    });
````

Events can be added/removed with the on and off methods, just like you would in jQuery.
Event delegation is also possible when you use the jQuery plugin.

````js
    $('#test_el').hammer().on("tap", ".nested_el", function(event) {
        console.log(this, event);
    });
````

### Gesture events
The following gestures are available, you can find options for it in gestures.js

- hold
- tap
- doubletap
- drag, dragstart, dragend, dragup, dragdown, dragleft, dragright
- swipe, swipeup, swipedown, swipeleft, swiperight
- transform, transformstart, transformend
- rotate
- pinch, pinchin, pinchout
- touch (gesture detection starts)
- release (gesture detection ends)


### Gesture options
The following gestures are available, you can find options for it in gestures.js

    doubletap_distance: 20
    doubletap_interval: 300
    drag: true
    drag_block_horizontal: false
    drag_block_vertical: false
    drag_lock_to_axis: false
    drag_max_touches: 1
    drag_min_distance: 10
    hold: true
    hold_threshold: 3
    hold_timeout: 500
    prevent_default: true
    release: true
    show_touches: true
    stop_browser_behavior: Object
    swipe: true
    swipe_max_touches: 1
    swipe_velocity: 0.7
    tap: true
    tap_max_distance: 10
    tap_max_touchtime: 250
    touch: true
    transform: true
    transform_always_block: false
    transform_min_rotation: 1
    transform_min_scale: 0.01


### Event data
The ````event```` argument in the callback contains the same properties for each gesture, making more sense for some than for others.
The gesture that was triggered is found in ````event.type````. Following properties are available in ````event.gesture````

    timestamp   {Number}        time the event occurred
    target      {HTMLElement}   target element
    touches     {Array}         touches (fingers, mouse) on the screen
    pointerType {String}        kind of pointer that was used. matches Hammer.POINTER_MOUSE|TOUCH
    center      {Object}        center position of the touches. contains pageX and pageY
    deltaTime   {Number}        the total time of the touches in the screen
    deltaX      {Number}        the delta on x axis we haved moved
    deltaY      {Number}        the delta on y axis we haved moved
    velocityX   {Number}        the velocity on the x
    velocityY   {Number}        the velocity on y
    angle       {Number}        the angle we are moving
    direction   {String}        the direction we are moving. matches Hammer.DIRECTION_UP|DOWN|LEFT|RIGHT
    distance    {Number}        the distance we haved moved
    scale       {Number}        scaling of the touches, needs 2 touches
    rotation    {Number}        rotation of the touches, needs 2 touches *
    eventType   {String}        matches Hammer.EVENT_START|MOVE|END
    srcEvent    {Object}        the source event, like TouchStart or MouseDown *
    startEvent  {Object}        contains the same properties as above,
                                but from the first touch. this is used to calculate
                                distances, deltaTime, scaling etc

### Custom gestures
You can write your own gestures, you can find examples and documentation about this in gestures.js.



## Compatibility
|                                   | Tap | Double Tap | Hold | Swipe | Drag | Multitouch |
|:----------------------------------|:----|:-----------|:-----|:------|:-----|:----------|
| **BlackBerry**                                                                         |
| Playbook                          | X   | X          | X    | X     | X    | X         |
| BlackBerry 10                     | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **iOS**                                                                                |
| iPhone/iPod iOS 6                 | X   | X          | X    | X     | X    | X         |
| iPad/iPhone iOS 5                 | X   | X          | X    | X     | X    | X         |
| iPhone iOS 4                      | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **Android 4**                                                                          |
| Default browser                   | X   | X          | X    | X     | X    | X         |
| Chrome                            | X   | X          | X    | X     | X    | X         |
| Opera                             | X   | X          | X    | X     | X    | X         |
| Firefox                           | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **Android 3**                                                                          |
| Default browser                   | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **Android 2**                                                                          |
| Default browser                   | X   | X          | X    | X     | X    |           |
| Firefox                           | X   | X          | X    | X     | X    |           |
| Opera Mobile                      | X   | X          | X    | X     | X    |           |
| Opera Mini                        | X   |            |      |       |      |           |
|                                                                                        |
| **Windows 8**                                                                          |
| Internet Explorer 10              | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **Windows Phone 8**                                                                    |
| Internet Explorer 10              | X   | X          | X    | X     | X    | X         |
|                                                                                        |
| **Windows Phone 7.5**                                                                  |
| Internet Explorer                 | X   |            |      |       |      |           |
|                                                                                        |
| **Other devices**                                                                      |
| Kindle Fire                       | X   | X          | X    | X     | X    | X         |
| Nokia N900 - Firefox 1.1          | X   |            |      |       |      |           |
|                                                                                        |
| **Windows Dekstop**                                                                    |
| Internet Explorer 7               | X   | X          | X    | X     | X    | X*        |
| Internet Explorer 8               | X   | X          | X    | X     | X    | X*        |
| Internet Explorer 9               | X   | X          | X    | X     | X    | X*        |
| Internet Explorer 10              | X   | X          | X    | X     | X    | X*        |
|                                                                                        |
| **OSX**                                                                                |
| Firefox                           | X   | X          | X    | X     | X    | X*        |
| Opera                             | X   | X          | X    | X     | X    | X*        |
| Chrome                            | X   | X          | X    | X     | X    | X*        |
| Safari                            | X   | X          | X    | X     | X    | X*        |
|                                   | **Tap** | **Double Tap** | **Hold** | **Swipe** | **Drag** | **Multitouch** |

Android 2 doesn't support multi-touch events, so there's no transform callback on these Android versions.
Windows Phone 7.5 doesnt support touch and minimal mouse events.

Not all gestures are supported on every device. This matrix shows the support we have tested. This is of course far from extensive.
If you've tested hammer.js on a different device, please let us know.

*Multitouch gestures are available with the hammer.fakemultitouch.js plugin.


## Todo
- Update website in gh-pages
- Write tests


## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style.
Add unit tests for any new or changed functionality. Lint and test your code using grunt.
Please don't commit the dist versions with your changes, only the changed source files.


## Further notes
Created by [Jorik Tangelder](http://twitter.com/jorikdelaporik) and developed at [Eight Media](http://www.eight.nl/) in Arnhem, the Netherlands.

It's recommend to listen to [this loop](http://soundcloud.com/eightmedia/hammerhammerhammer) while using hammer.js.
