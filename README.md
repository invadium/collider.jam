<p align="center">
<a href="https://github.com/invadium/collider.jam">
<img src="res/logo-big.png" width="160">
</a>
</p>


Welcome to Collider.JAM!
========================

**[collider.land](https://collider.land)
| [start](https://collider.land/help/#.getting-started)
| [design](https://collider.land/help/#design)
| [docs](https://collider.land/help/)
| [blog](https://ikhotin.com/posts/)
| [discord](https://discord.gg/kxNnHc2)**

---

```
npm install -g collider.jam
```

<p align="right">
    <i><b>🎮 Crafting games with joy. 🎮</b></i>
</p>

**Collider.JAM** is a hand-crafted JavaScript framework
for game jamming, creative coding, indie development, and beyond.
It is _free_, _open-source_, and fun to create with.
**Collider.JAM** originates from countless game jams and years of indie game development, bringing a unique, flexible, and powerful way of game production. _The jamming way!_
Find out more at [collider.land](https://collider.land).

---

Install **Collider.JAM** with ```npm i -g collider.jam``` and check out [online documentation](https://collider.land/help/). Explore _Collider.JAM_ [code examples](#examples) and [jam game sources 🎮](#full-games-with-sources).

👾 _Follow the jamming way and pixelate reality!_ 👾

---

Table of Contents
-----------------
* [Install](#install)
* [Game Jamming](#game-jamming)
* [Bouncing Planet](#bouncing-planet)
    * [Draw Shape](#draw-shape)
    * [Move Shape](#move-shape)
    * [Prototype in Development Mode](#prototype-in-development-mode)
    * [Drop Resource](#drop-resource)
    * [Handle Mouse](#handle-mouse)
    * [Things to Try](#things-to-try)
* [Explore](#explore)
* [Examples](#examples)
* [Full Games with Sources](#full-games-with-sources)
* [How to Contribute](#how-to-contribute)
* [License](#license)



Install
-------
<p align="right">
    <i><b>Unlock your creativity.</b></i>
</p>

To start jamming, install the _collider.jam npm package_.
It provides a shell for bootstrapping, running, and packaging projects.

---

Make sure you have a relatively modern
_[Node.js](https://nodejs.org)_ and _npm_ installed (check ```node --version```).

To install **Collider.JAM** run the following command in the system terminal:

```
npm install -g collider.jam
```

When installed, open the local manual to explore potential next steps:

```
jam man
```

There you can read more about **Collider.JAM**, find out how to use it, explore code examples and tutorials, and browse other included reference materials.


Game Jamming
------------

_Game jamming_ is an art form that mixes design, technology, creativity, and hyper-focused productivity.
It is a way of software development that is radically different from a typical approach one might find in other fields.
And we believe it deserves a dedicated tool, capable of addressing the specific needs of a rapidly evolving prototype and the creative flow that powers it.

**Collider.JAM** takes JavaScript dynamism to the extreme, delivering a framework radically different from a typical approach.

There is no _GameObject_ to inherit, no _MonoBehavior_ to implement, no imports, no exports, no resource loading... None of that industrial-grade object-oriented nonsense plaguing the game industry and creating unnecessary noise.

Instead, **Collider.JAM** offers reasonable conventions, dynamic in-place binding of context, short UNIX-style names, and automatic imports, exports, and loads.

So [explore](https://collider.land/help/) **Collider.JAM** JavaScript majik, find out when is the next interesting [game jam](https://itch.io/jams) and create something awesome!

_Or you can start with creating a bouncing planet._



Bouncing Planet
---------------
<p align="right">
    <i><b>🎮 The Fun of Game Jamming. 🎮</b></i>
</p>

To feel the taste of _Collider.JAM_, let's create a simulation of a bouncing planet.


### Draw Shape

Create a folder named 'planet.mod' in any convenient place
```
mkdir planet.mod
```

The *.mod* extension is crucial,
since that is how **Collider.JAM** determines
the root of the project.
**Collider.JAM** has particular conventions
on how you name and organize files and directories.

It could be unusual at first, but it makes a lot of sense
once you get into the jamming mode.

---

Create a file *planet.mod/lab.js* and fill in the following lines:

```js
// planet.mod/lab.js

function draw() {
    lineWidth(2)         // set the line width
    stroke(.12, .4, .5)  // color in float HSL
    circle(200, 200, 50) // draw the circle
}
```

Now, run the ```jam play``` command while inside the *planet.mod* folder:
```
jam play
```

Collider.JAM will start a server and open the default browser, 
pointing at [http://localhost:9999](http://localhost:9999).
You should see the circle.

---



### Move Shape

Let's make some movement by introducing
variables for the circle position and direction.
We also need the *evo(dt)* function to move it:

```js
// planet.mod/lab.js

// position at the center of the screen
let x = rx(.5)
let y = ry(.5)
let r = 50

// the speed along x and y axes
let dx = 100
let dy = 100

function evo(dt) {
    // dt(delta time) holds the time in seconds passed since the last update
    //move factored by the delta time
    x += dx * dt
    y += dy * dt
}

function draw() {
    lineWidth(2)
    stroke(.12, .4, .5)   // color in float HSL
    circle(x, y, r)
}
```

The problem is that the circle disappears
once it crosses the edge of the screen.

We can introduce some boundaries on x and y,
so our evo(dt) would look like this:
```js
function evo(dt) {
    // make the movement factored by the delta time
    x += dx * dt
    y += dy * dt

    // bounce off the screen edges
    if (x > rx(1)-r && dx > 0) dx *= -1
    else if (x < r && dx < 0) dx *= -1
    if (y > ry(1)-r && dy > 0) dy *= -1
    else if (y < r && dy < 0) dy *= -1
}
```

Find the working example on [GitHub](https://github.com/invadium/bits.mix/tree/master/circle.mod).

---


### Prototype in Development Mode

The simplest *Collider.JAM* command is _jam_:

```
jam
```

It runs the jam server without opening a web browser,
unlike *jam play*, which does.

But when it comes to development, it's much better
to run in the _debug mode_:

```
jam -d
```

That enables hot reload of changes
and the help metadata, among other things.

Run *Collider.JAM* with -d option,
then open the browser at http://localhost:9999
and try to change the circle color or radius.

The changes will be visible in the browser
soon after you save ```lab.js```.

Also, you can hit F1 and get online help
on everything in the mix, including
Collider.JAM utilities and your code!



### Drop Resource

Let's improve our bouncing circle.

Find a suitable image of a planet with a transparent background,
just like
[this one](https://opengameart.org/sites/default/files/mars_type_planet.png)
from [OpenGameArt](https://opengameart.org).
Or pick any planet from [this procedurally generated collection](https://github.com/invadium/procedural-november.pak/tree/main/planets).


Download and drop it into the *planet.mod/res/* folder.

Now add init() and change the draw() function to the following:

```js
function init() {
    this.background = '#000000' // black color in hex RGB
}


function draw() {
    lineWidth(5)
    stroke(.58, .5, .7)
    circle(x, y, r)
    image(res.mars_type_planet, x-r, y-r, 2*r, 2*r)
}
```

We've changed the background to totally black to match the darkness of space.

Then, we called the _image()_ function to draw the planet's texture.
Notice that the image resource name must match
the file name without the extension.
It is the way resources are mapped and loaded.

We've preserved the circle and tuned its width and color to resemble
the planet's atmosphere.

Check out this step on [GitHub](https://github.com/invadium/bits.mix/tree/master/planet.mod) -
the version there also spins the planet with *save()/rotate()*.

---


### Handle Mouse

Suppose our planet is slowing down.

Add the following function to reduce the speed:
```js
function slowDown(dt) {
    dx *= 1 - 0.05*dt
    dy *= 1 - 0.05*dt
}
```

And call it from evo(dt) like that:
```js
function evo(dt) {
    ...
    slowDown(dt)
}
```

Now, the planet will lose 5% of its speed every second.

But we want it to accelerate on click,
so we will include boost() function:
```js
function boost(mouseX, mouseY) {
    if (!this.booster && distance(x, y, mouseX, mouseY) <= r) {
        dx *= 1.2
        dy *= 1.2
        this.booster = true
    }
}
```

We are checking if the mouse coordinates are within
the planet's radius and make a 20% speed increase if so.
The *booster* flag is needed for visual feedback.
We want to show the player a hint
that the boost has actually happened.

For example, we can change the atmosphere color
in draw():
```js
function draw() {
    lineWidth(5)
    if (this.booster) stroke(.05, .4, .6)
    else stroke(.58, .5, .7)
    circle(x, y, r)
    image(res.mars_type_planet, x-r, y-r, 2*r, 2*r)
}
```

It is time for mouse handling.
Create a folder named *trap* and place
two .js files there - *mouseDown.js* and *mouseUp.js*.

Put in *mouseDown.js*:
```js
// planet.mod/trap/mouseDown.js

function mouseDown(e) {
    lab.boost(e.clientX, e.clientY)
}
```

And *mouseUp.js* is going to be:
```js
// planet.mod/trap/mouseUp.js

function mouseUp() {
    lab.booster = false
}
```

Try it out - the planet is going to accelerate
on mouse click. 

Find the complete example on [GitHub](https://github.com/invadium/bits.mix/tree/master/planet-boost.mod).
---

The _jamming way_ is that simple!

Just place the files in proper folders,
follow naming conventions and
Collider.JAM will assemble and run
the game for you.



### Things to Try

Open the mix inspector by pressing **F2**.
Explore the existing structure and try to find your custom nodes there.
Keep in mind that the mix follows the directory structure,
so things you placed in the */lab* folder will be in the */lab* node.

Open the debug console with **F4** and type "help" to see commands available out of the box.



Examples
--------

There are useful _Collider.JAM_ examples on GitHub:

* [Bits Mix](https://github.com/invadium/bits.mix) - various code snippets.
* [Hello Planet Impact](https://github.com/invadium/hello-collider-impact.mod) - asteroid impact simulation.
* [Pong](https://github.com/invadium/pong-ce.mod) - classic arcade reimplementation.
* [Vector Zone](https://github.com/invadium/vector-zone.mod) - local multiplayer arcade shooter.
* [Game of Life](https://github.com/invadium/game-of-life.mod) - Conway's Game of Life.



Full Games with Sources
-----------------------
<p align="right">
    <i><b>Follow the jamming way</b></i>
</p>

Explore the following games. All created during various game jams and powered by *[_Collider.Jam_](https://collider.land)*.

*Note that older games could use old-style or deprecated features.
But mostly they are OK and show many different ways to organize a project in Collider.JAM.*

* [Telemetry Troubles](https://github.com/invadium/telemetry-troubles.mix) - *[Play](https://invadium.itch.io/telemetry-troubles)* - programming puzzle game created for Noise Jam 3 (2026).
* [Enceladus Dockyards Boy](https://github.com/invadium/enceladus-dockyards-boy.mix) - *[Play](https://invadium.itch.io/enceladus-dockyards-boy)* - turn-based spaceship battle simulation from GameBoy Jam 8 (2020).
* [Jump 'N Loop](https://github.com/invadium/jump-n-loop.mod) - *[Play](https://invadium.itch.io/jump-n-loop)* - rhythm-based runner from Ludum Dare 47.
* [300 Hearts for Escape](https://github.com/invadium/300-hearts-for-escape) - *[Play](https://ingwar.itch.io/300-hearts-for-escape)* - a survival trading game set on an isolated island created during Ludum Dare 44.
* [Plume Surfing Day](https://github.com/invadium/plume-surfing-day.mix) - *[Play](https://invadium.itch.io/plume-surfing-day)* - a god-game about little creatures colonizing asteroids on volcanic plumes made for Brackeys Game Jam 2025/1.
* [Station Keeping](https://github.com/invadium/station-keeping.mod) - *[Play](https://invadium.itch.io/station-keeping)* - space survival trading simulation from Ludum Dare 46 (2020).
* [Cosmic Rays 'n DNAs](https://github.com/invadium/cosmic-rays-n-dnas.mod) - *[Play](https://ingwar.itch.io/rays)* - fix DNA in this arcade Global Game Jam 2020 Entry.
* [Mech Force Command](https://github.com/invadium/mech-force-command.mix) - *[Play](https://invadium.itch.io/mechanized-force-command)* - 7-Day Roguelike Challenge 2021 Entry
* [Xeno Relay Day](https://github.com/invadium/xeno-relay-day) - *[Play](https://ingwar.itch.io/xeno-relay-day)* - cosmic relay network puzzler created during Global Game Jam 2018.
* [Metro Gang](https://github.com/invadium/metro-gang.mix) - *[Play](https://invadium.itch.io/metro-gang-plus)* - fight against rival gangs for control of the city in this Ludum Dare 45 Entry.
* [Master of Ritual](https://github.com/invadium/master-of-ritual) - *[Play](https://ingwar.itch.io/master-or-ritual)* - dungeon crawler from Ludum Dare 43 (2018).



Explore More
-------------

The following links could be useful:

* [collider.land](https://collider.land)
* [online help](https://collider.land/help/)
* [design](https://collider.land/help/#design)
* [how to](man/HowTo.md)
* [map](man/Map.md)
* [glossary](man/Glossary.md)
* [blog](https://ikhotin.com/posts/)



How to Contribute
-----------------

Star this repo, join our [Discord](https://discord.gg/kxNnHc2),
create something and share it with *#collider.jam* tag.

Check out [how to develop Collider.JAM](man/Development.md).

More details in **[How to Contribute](CONTRIBUTING.md)**.



License
-------

_Collider.JAM_ is free and open-source software released under the
[Zlib License](LICENSE).
Bundled resources are covered separately - see [LICENSE-RES](https://github.com/invadium/collider.mix/blob/master/LICENSE-RES) in _collider.mix_.


