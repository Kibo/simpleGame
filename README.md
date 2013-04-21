Overview of SimpleGame
=====================

###The simpleGame.js library was designed with a few key features in mind:

* **Ease of learning** – Perhaps the most important design goal was to create a library that is easy to learn and use. The library has a relatively small number of objects, and it strives to use straightforward language whenever possible
* **Hiding complexity** – Game programming often requires a great deal of complexity. HTML5 game development can be especially tricky. Many of the concepts needed in a game engine (collision detection, sound effects, vector projection) involve complex math and programming, which is hidden from the game developer when possible.
* **Platform-agnostic** – The library was designed to work as well as possible on many platforms. It works on most modern browsers as well as mobile devices.
* **Mobile-friendly** – The library aims to support not only traditional desktop web browsers, but also mobile devices like cell phones and tablets.
* **Reasonably powerful** – On a modern computer, the library can perform about as well as many other web and mobile gaming platforms, including Flash.
* **Object-oriented** – the library uses objects throughout, with a consistent scheme. All the main features are supported by an appropriate object, which has properties and methods which allow you to manipulate the object.
* **Free and open source** – The simpleGame.js library is available for anyone to use for free. You can also modify the library and add your own features.

The Scene Object
===============

The central object of the simpleGame library is the Scene. When you create a Scene object, two primary things happen: The Scene creates a canvas tag to hold all the visual aspects of the game, and it begins a timing loop that causes a function called update() to run twenty times per second.

You should create the Scene object variable as a global variable so it is available to all functions. You'll normally initialize Scene as the first line of your init() function. The Scene constructor requires no parameters. The Scene object is first described in chapter 5, with more features described throughout the book.

Primary properties of the Scene object
================================

###The Scene object has a number of interesting properties you can read directly:

* **touchable** – The touchable property returns true when the browser detects a touch screen, and false when there is no touch screen. This is an ideal way to determine if the game is currently being run on a mobile device. You should never change this property directly. Just use it to determine if the current device has a touch interface (usually with an if statement.)
* **canvas** – The canvas property provides a reference to the canvas element produced by the scene. You can directly modify the canvas element (changing its size, for example,) but it's much better to use the various methods provided for this purpose.
* **height, width** – These two properties show the current height and width of the game area. Use the setSize() method to assign new values to height and width
* **top, left** – These two properties are used to describe the current position of the playing area's top-left corner. Use the setPosition() method to change the position of the game surface.

Important methods of the Scene class
===============================

###Like most objects, the Scene object is controlled with methods, which are used to manage the scene and change its behavior and appearance.

* **start()** - The start() method is used to begin the game. Normally you'll call the start() method at the end of the page's init() function, triggering the beginning of the game. The start() method adds the canvas to the page and begins the timing loop, which causes update() to be called twenty times per second. See chapter 5 for more information on initializing a scene.
* **clear()** - This method clears the canvas, drawing the background color (see setBackground() to change the background color.) Typically you'll call clear() at the beginning of the update() function. Failing to clear the scene can lead to trails of sprites drawn on the playing surface. Chapter 5 describes how to use the clear() method
* **stop()** - The stop() function is used to end the game. The timing loop is no longer called, but the screen pauses. If you want to clear the screen, call clear() before stopping the game. If you want to reset the game, the easiest way is to reload the page: document.location.href = “” You can learn more about stopping and restarting the game in chapter 7.
* **setSize(width, height)** – This method changes the size to the given width and height (measured in pixels) It may be necessary to adjust the size to make your game work well on mobile devices. This function is illustrated in chapter 9.
* **setPos(left, top)** – This method changes the position of the game surface to the given values.
* **setSizePos(width, height, left, top)** – A utility function which allows you to change the size and position at the same time.
* **setBG(color)** - This method changes the background color of the playing area. You can use any of the normal CSS color values (named colors or hex values.) The game canvas is repainted to the indicated color every time the scene's clear() method is activated.
* **hideCursor()** - This method allows you to hide the mouse cursor. It is especially useful when the game uses mouse or touch-screen information as an input.
* **showCursor()** - The showCursor() method makes the ordinary mouse cursor visible again after being hidden by hideCursor(). The cursor methods are detailed in chapter 9.
* **getMouseX(), getMouseY()** - These two methods are used to return the position of the mouse on the game canvas. Note that these methods (unlike the Joystick variations of the same methods) compensate for the position of the canvas. Mouse and Joystick techniques are fully discussed in chapter 9.
* **hide()** - Hides the game canvas. This is useful when you want to use the game's timing loop but you don't necessarily want to show the canvas. (I used this for a few examples throughout the book when the canvas itself wasn't needed.)
* **show()** - Displays the game canvas after it has been hidden by hide()

The Sprite Class
=============

Scenes provide the background of a game, but the other key element in simpleGame is the Sprite class. Nearly every game element is based on the sprite, so understanding what the sprite can do is the key to writing games in simpleGame. The Sprite class is first introduced in chapter 5, and it is further described throughout the book.

The sprite class is quite large, so the various properties and methods are broken into several different categories.

The sprite constructor has a number of important parameters:

    mySprite = new Sprite(scene, imageFile, width, height)

Each sprite should be created as a global variable, and the sprites should all be initialized in the init() method. You must indicate all the required parameters when creating a sprite:

* **scene** – Sprites are always associated with a given Scene. Generally you'll create a Scene first, and then create sprites attached to that scene
* **imageFile** – This is the file name of the image the sprite will be based upon. Typically this will be a smaller image in a web-friendly format (gif, jpg, or png.) Usually you'll want to design your sprites so they face East by default. This will cause the direction properties to work as expected.
* **width, height** – these are the width and height of the sprite.

Main properties of the Sprite
=======================

The sprite has a number of properties. You can read values from these properties, but it's best not to change them directly. Instead, use the appropriate method to change the behavior or appearance of a sprite. Basic sprite methods are described in chapter 5, but you'll see more advanced techniques used throughout the book, especially in chapter 8.

* **canvas** – The canvas element upon which the sprite is drawn.
* **width, height** – The width and height of the sprite. Important not only for the visual display of the element, but in collision detection
* **cWidth, cHeight **– Size of the canvas containing the element. This information can be useful when you make a custom boundary action. See checkBounds() method for more information.
* **x, y** – position of the sprite. Do not change these values directly, but use one of the many sprite motion mechanisms. However, you can use these properties to discover the current position of the sprite.
* **dx, dy** - motion of the sprite. Do not change these values directly, but you can use these properties to determine how quickly the sprite is moving vertically (dy) or horizontally (dx.)
* **speed** – You can use this property to view the speed of the sprite, but do not change it directly. Instead, use one of the speed methods described later.

Appearance methods of the Sprite
============================

Use these methods to change the appearance of the Sprite element

* **changeImage(imgFile)** – Changes the image to the image file. The file should be in a web-safe format, and should not be larger than the intended display size.
* **setImage(fileName)** – Another name for changeImage(). Works exactly like changeImage()
* **update()** - This method draws the sprite on the screen. Typically you will update each sprite at the end of the main program's update() function. Sprites which are updated first appear at the bottom of the screen, so if you want a sprite to appear above another sprite, update it later.
* **hide()** - hides the sprite. The sprite will still calculate speed and position, but it will not be displayed on the screen, and it will not collide with other sprites.
* **show()** - This function displays a sprite that was hidden with the hide() method
* **report()** - This is a utility method that displays the current position, dx, dy, speeed, and angle to the debugging console. It is intended only for debugging purposes, but can be quite handy when you are trying to discover what a sprite is supposed to be doing.

Movement Methods of the Sprite
===========================

One of the most important jobs of the sprite object is to move around the screen in interesting ways. At its very essence, position is stored as an (x, y) coordinate pair. You can directly set the position of the sprite, but there are many convenience methods which give you better control of sprite motion. The basic motion format is a motion vector (dx, dy.) You can set these values directly with appropriate methods, but sprites also have speed and angle attributes which can give much more interesting behavior. In fact, a sprite has two different angle measurements, the imageAngle, and the moveAngle. The imageAngle determines which direction the sprite is facing, and the moveAngle determines the direction of motion. If you simply change the angle, you are changing both the image and movement angles at once. All angles in simpleGame are measured in degrees using normal navigation formatting, with 0 degrees pointing up and 90 degrees pointing to the right.

* **setPosition(x, y)** – immediately changes the position of the sprite to the give x and y coordinates.
* **setX(newX), setY(newY)** – Allows you to change X and Y to some new value.
* **setDX(newDX), setDY(newDY)** – Change motion in X or Y axis. If you set the dx value to 5, for example, the sprite will move 5 pixels to the right every frame until the dx value is changed again. The angle and speed settings of the sprite will be effected by changes in dx and dy. (This is why you must always use functions to change dx and dy – if you change the properties directly, the speed and angle will no longer be accurate.)
* **changeXby(newDX), changeYby(newDY)** – Alternate names for setDX() and setDY()
* **setSpeed(speed)** – sets the speed to the indicated value. Speed is determined in pixels per frame. You can set speed to a positive or negative value. The speed will change immediately with this method. If you want a more realistic change in speed, use changeSpeedBy() or addVector().
* **getSpeed()** - Returns the current speed based on the current settings of dx and dy.
* **changeSpeedBy(diff)** – Changes the speed by the diff amount. A positive value will cause the sprite to speed up in the moveAngle direction, and a negative value will slow the sprite down. It is possible to attain negative speeds, which will cause the sprite to move backwards. You may want to assign top and bottom speeds to keep your sprite from moving so quickly that it is difficult to control.
* **setImgAngle(degrees)** – Changes the angle at which the sprite is drawn. DOES NOT affect the motion angle. Use this mechanism to rotate a sprite without changing its direction of travel. The degrees value should be an integer between 0 and 360, but larger and smaller values will be accepted and adapted to appropriate values. This method immediately turns to the indicated angle. Use changeImgAngleBy() for animated rotation.
* **changeImgAngleBy(degrees)** – Changes the image angle by the indicated degree measurement. Use a positive value to rotate the sprite clockwise, and a negative number to rotate counter-clockwise.
* **getImgAngle()** - Returns the sprite's current image angle in degrees.
* **setMoveAngle(degrees)** – Immediately sets the sprite's motion angle to the indicated angle. Does not affect visual rotation of the image, so this can be used when you want to decouple the direction a sprite is pointing and the angle at which it travels (This technique is frequently used for skidding behavior, for example.)
* **changeMoveAngleBy(degrees)** – Changes the movement angle by the indicated amount. Used to modify the motion angle over time.
* **getMoveAngle()** - Returns the sprite's current motion angle in degrees.
* **setAngle(degrees)** – A utility function that sets both the image and motion angle. Used when the sprite will be traveling in the same direction it is pointing (as in most simple driving games without skidding.)
* **changeAngleBy(degrees)** – Change both the motion and image angle at the same time. Used to turn the sprite gradually.
* **turnBy(degrees)** – Another name for changeAngleBy()
* **addVector(degrees, thrust)** – A very powerful method that adds a motion vector to the current sprite. The function applies a vector in the direction indicated by degrees, and with the force indicated by thrust. Skillful use of this method can lead to many interesting physics-based behaviors. See chapter 8 for a complete examination of this flexible method, which is used for gravity, skidding, and orbits, among other things.

Boundary methods of the sprite
==========================

With all this movement, it isn't surprising that sprites sometimes leave the confines of the game canvas. Most boundary-handling behavior is automatic, but you can either change the default boundary-checking mechanism, or you can add your own. Note that each sprite has a different boundary-checking behavior, so you can have more than one boundary mechanism in the same game. (bullets frequently die when they leave a screen, while spacecraft may wrap around, for example.)

* **setBoundAction(action)** – Determines what the sprite will do when it hits a screen boundary. The action value can be one of the following:
  * **WRAP** – The sprite will keep the same speed and angle, but will appear on the opposite of the side it left. So if a sprite leaves the left side of the screen, it will appear on the right, but the speed and direction of travel will remain the same. WRAP is the default bound action.
  * **BOUNCE** – The sprite will stay in the same spot, but its direction will be reversed. If it bounces off the top or bottom of the canvas, the dy value is inverted. If it bounces off the left or right of the canvas, the dx value is inverted.
  * **STOP** – The sprite's speed will be set to zero and the sprite will stay at the spot where it left the screen. It may appear only partially on- screen. If you want a stopped sprite to move again, you'll need to change its direction, position, or boundaction.
  * **DIE** – The sprite will stop moving and will be hidden. It is not removed from memory, but it will no longer be displayed, nor will it register collisions.
  * **CONTINUE** – The sprite will continue to travel beyond the visible canvas. This option should only be used when there is some way of getting the sprite back (as in an orbit demonstration, or when the off-screen coordinates are displayed, like in an air-traffic control simulation.) If the boundAction is set to some value the game engine does not recognize, CONTINUE will be set.
* **checkBounds()** - The checkBounds() function automatically uses the indicated bound action. If you need a custom bound action (for example you want to wrap off the top and bottom but bounce off the sides) you can create your own checkBounds() method. However, you are then completely responsible for ensuring your method handles all the possible boundary conditions. Never call checkBounds() directly (it is already called at the appropriate moment) but overwrite it if you need some sort of fancy boundary-checking behavior.

Collision methods of the Sprite
=========================

The sprite has two main ways to check collisions. There is a standard collidesWith() method which checks for bounding-rectangle collisions. In addition, you can use the distanceTo() and angleTo() methods to get a better sense of the proximity of two sprites. Chapter 6 describes collision-detection in some detail.

* **collidesWith(sprite)** – Returns true if this sprite's bounding rectangle is currently overlapping the given sprite's bounding rectangle. Note that this is a very fast collision routine, but it is not pixel-perfect. In particular, long-thin sprites will have very different collision behaviors if they are diagonal, vertical, or horizontal. If you need more uniform collision mechanism, use the distanceTo() method instead. If either sprite is invisible, a collision will not be registered.
* **distanceTo(sprite)** – Returns the distance (in pixels) between this sprite and the target sprite. Useful for boundary-circle checking. If the distance between two sprites is less than some threshold, count it as a collision. Unlike the standard collidesWith() mechanism, the distance-based collision technique works the same regardless of the sprites' orientations. This method works whether the sprites are visible or not.
* **angleTo(sprite)** – Returns the angle (in degrees) from the current sprite to the given sprite. Use this method to have a 'guided missile' that always points to a target, or to apply a gravity vector between a planet and a spacecraft. This method works whether the sprites are visible or not.

Animation methods of the Sprite
==========================

The simpleGame library has limited support for spritesheet animations. See chapter 8 for a description of this technique. The following methods assist with Animations:

* **loadAnimation(width, height, cellWidth, cellHeight)** – Indicates that the image associated with the sprite is actually a sprite sheet. The first two parameters indicate the size of the overall sprite sheet, and the second two values indicate the width and height of a single cell within the sheet.
* **generateAnimationCycles()** - generates a series of animation cycles. Default behavior presumes each row is a new state and each column is an animation within that state. Typically rows indicate directions and columns indicate cells within the animation.
* **renameCycles(cycleNameArray)** – This method allows you to set string names to each of the cycles. Typically these will indicate directions or behaviors.
* **setAnimationSpeed(speed)** – This method indicates how quickly the animation will cycle. Setting a higher value will slow down the animation.
* **setCurrentCycle(cycleName)** – Changes the animation cycle to the one indicated by the cycle name. Normally used to change animation state.
* **playAnimation()** - begins (and repeats) the currently indicated animation.
* **pauseAnimation()** - Pauses the animation until it is re-started with a playAnimation() command.

Utility Classes
===========

In addition to the main two classes, the simpleGame library includes a number of helpful utility classes. Use these classes to add features to your game, from sound effects to mobile device interface schemes.

The Sound Object
===============

The sound class encapsulates the HTML5 audio object, and makes it very easy to build sound effects. When you build a sound object, you'll actually be creating an HTML5 audio object which is not displayed, but can be played with JavaScript code. Note that the sound object has the same limitations as HTML5 sound elements. Most importantly, there is no single audio format guaranteed to play on every browser. For best results, create each sound effect twice (once in .mp3 and once in .ogg format) and create a Sound object for each. Use of the Sound object is described in chapter 6.

* **sndElement** = new Sound(src) – Creates a new sound object. Generally, you'll want to store the sound in a global variable. The src attribute indicates the file name of the sound. For maximum effectiveness, create two objects for each sound effect (one in mp3, one in ogg.)
* **play()** - Plays the sound effect encapsulated by the sound.
* **showControls()** - Shows the HTML5 control panel (a play button and a simple timer) for the sound effect. By default, controls are turned off. This option was added as a workaround for an issue with iPhone and iPad browsers.

Note that the iPhone / iPad operating systems have a well-known problem playing back sound effects from JavaScript. IOS (the iPhone / iPad / iPod operating system) refuses to preload a sound, and will only load the sound effect after direct user feedback. In practice, this means you cannot load a sound in the background. However, there is a loophole. Use the sound object's showControls() method to make the HTML5 audio control panel appear for each sound. The user can then manually load each sound by playing it once. Once the sound is in memory, it will play within the game with no problems. Each time the page is reloaded, you will need to reload the sounds.

See Chapter 6 for complete details on how to use the sound object.

The Timer Object
==============

The timer is a simple object designed to give you an easy way to work with elapsed time. It only has two methods, and they are both quite straightforward:

* **reset()** - This command resets the timer. Use it whenever you want to begin counting some amount of time.
* **getElapsedTime()** - This method returns the number of seconds since the timer was started or reset.
If you look at the source code, you'll find another method getCurrentTime() but this is only used internally, and is not likely to be useful as it is. (It returns the current time in a format that's useful for calculations, but not human-readable)

The timer is explained in chapter 6.

The Virtual Joystick
================

One of the most interesting features of the simplegame library is its support for mobile devices. Since these devices often do not have keyboards, they rely on alternative input methods. The virtual joystick object is used to manage touchscreen input.

* **joystickName = new Joy()** - Create a virtual joystick object. Normally it's best to do this after checking for the touchable interface through the scene.touchable property. However, if you create a virtual joystick and the browser cannot support it, the joystick commands will simply be ignored.
* **getMouseX(), getMouseY()** - These methods return the x and y position of the touch. If a virtual joystick is turned on, the scene's getMouseX() and getMouseY() methods will reflect the mouse's position. Note that with a real mouse, there is always a value for mouseX and mouseY. With a touch interface, there is not a meaningful value for mouseX and mouseY unless the user is currently touching the screen. Chapter 9 details the use of the touch screen and mouse.
* **getDiffX(), getDiffY()** - Returns a value indicating how much the user has moved the mouse in X or Y since initially touching the screen. This is the foundation of the virtual joystick. See chapter 9 for details on using the virtual Joystick object.
* **virtKeys** – This is an ordinary variable. If you create a variable called virtKeys and set it to true before you create a virtual joystick, the joystick will automatically act like arrow keys. This is an easy way to build a multi-platform game. Use the arrow keys as the primary input interface, but add a virtKeys interface so mobile users can replace the keys with a virtual joystick. 

See chapter 9 for more detail on using the virtual joystick in this way.

The virtual Accelerometer
=====================

In addition to touch input, mobile devices also include support for motion-detection with a built-in accelerometer. The accelerometer measures rotation around all three axes, but x and y turn out to be most useful.

* **AccelName = new Accel()** - Build a new accelerometer object called accelName. If the device does not support an accelerometer, nothing will happen (so you'll want to include some other input type, like the keyboard or buttons.)
* **getAX()** - Get acceleration around the X axis. Note that the X axis is side-to-side, so acceleration around this axis will often map to changes in Y.
* **getAY()** - Get the acceleration around the Y axis, which is vertical. Normally you'll map acceleration around Y to changes in an object's X or dx values.
* **GetAZ()** - Technically, this reads acceleration around the Z axis, which runs from the center of the screen to the user's nose. In reality, this is rarely used, as these rotations will usually also trigger an acceleration around Y.
* **getRotX(), getRotY(), getRotZ()** - These utility functions indicate the amount of rotation around each of the axes since the last frame. They are provided as a service, but normally the getAX() and getAY() functions are sufficient for handling most rotation situations.

See chapter 9 for more information on how to use the accelerometer for motion-sensing.

The Game Button
===============

The game button provides a convenient button which can be used in both desktop and mobile games. It is essentially a standard HTML button, but it is optimized for game programming, especially on mobile devices as an alternative to keyboard input.

* **buttonName = new GameButton(label)** – Create a new button. The label text will become the text of the button.
* **setPosition(x, y)** – Sets the position of the button to the indicated screen coordinates. The button can be placed on the playing surface or anywhere else on the screen.
* **setSize(width, height)** – Sets the width and height of the button to the indicated values. Remember that buttons may be easier to hit if they are larger.
* **isClicked()** - Returns a true value if the button is currently clicked, or false if the button is not currently clicked. Use this method to easily check for button presses.

Note that the label can be any valid HTML text, including plain text or an image (using the standard <img> tag. You can also use CSS to style your labels (use the standard button style) to make them semi-transparent if you prefer. You can find complete discussion of the GameButton class in chapter 9.

Keyboard array
============

The keyboard is a primary input mechanism for the simpleGame engine, so it's designed to be easy to use. As soon as the Scene is initialized, a special array called keysDown is created. There is an entry in this array for each of the main keys on the keyboard. Check the status of a key by using the keyboard constant as the index. The keyboard constants all begin with a capital K, followed by an underscore and the letter name. EG the A key is K_A, and B is K_B. In addition to the letter and number keys, the following keyboard constants are defined:

* K_UP
* K_DOWN
* K_LEFT
* K_RIGHT
* K_SPACE
* K_ESC
* K_PGUP
* K_PGDOWN
* K_HOME
* K_END

Note that these keys are defined for a standard US keyboard, and some behavior may be different on different keyboards.

This system (unlike standard JavaScript keyboard techniques) allows for multiple keys to be pressed at one time.

Chapter 5 describes how to read the keyboard.

Credits
======

Book by Andy Harris - [HTML5 Game Development for Dummies](http://aharrisbooks.net/websitebaker/pages/books/html5-game-development.php)

Documentation from [http://aharrisbooks.net/h5g/documentation.html](http://aharrisbooks.net/h5g/documentation.html)

SimpleGame Practice Tool
======================
For practicing code examples in your browser, visit:

[http://aharrisbooks.net/h5g/simpleGamePractice.html](http://aharrisbooks.net/h5g/simpleGamePractice.html)

Examples
========

[http://aharrisbooks.net/h5g/](http://aharrisbooks.net/h5g/)
