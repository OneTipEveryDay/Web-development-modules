## Relationship between JavaScript, APIs, and other JavaScript tools

>[!IMPORTANT] <ul>
>  <li>JavaScript — A high-level scripting language built into browsers that allows you to implement functionality on web pages/apps. Note that JavaScript is also available in other programming environments, such as Node.</li>
>  <li>Browser APIs — constructs built into the browser that sit on top of the JavaScript language and allow you to implement functionality more easily.</li>
 >  <li>Third-party APIs — constructs built into third-party platforms (e.g., Disqus, Facebook) that allow you to use some of those platform's functionality in your own web pages (for example, display your Disqus comments on a web page).</li>
 > <li>JavaScript libraries — Usually one or more JavaScript files containing custom functions that you can attach to your web page to speed up or enable writing common functionality. Examples include jQuery, Mootools and React.</li>
>  <li>JavaScript frameworks — The next step up from libraries, JavaScript frameworks (e.g., Angular and Ember) tend to be packages of HTML, CSS, JavaScript, and other technologies that you install and then use to write an entire web application from scratch. The key difference between a library and a framework is "Inversion of Control". When calling a method from a library, the developer is in control. With a framework, the control is inverted: the framework calls the developer's code.
> </li>
> </ul>

## How do APIs work?

### They are based on objects

So how do these objects interact? If you look at our simple web audio example (see it live also), you'll first see the following HTML:

```js
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Basic Web Audio example</title>
    <style>
      input {
        height: 1.5em;
      }
    </style>
  </head>
  <body>
    <audio src="outfoxing.mp3"></audio>

    <button class="paused">Play</button>
    <br />
    <input type="range" min="0" max="1" step="0.01" value="1" class="volume" />

    <script>
      // Create an AudioContext (cross browser)
      const AudioContext = window.AudioContext || window.webkitAudioContext;
      const audioCtx = new AudioContext();

      // store references to our HTML elements
      const audioElement = document.querySelector("audio");
      const playBtn = document.querySelector("button");
      const volumeSlider = document.querySelector(".volume");

      // load the audio source into our audio graph
      const audioSource = audioCtx.createMediaElementSource(audioElement);

      // play/pause audio
      playBtn.addEventListener("click", () => {
        // check if context is in suspended state (autoplay policy)
        if (audioCtx.state === "suspended") {
          audioCtx.resume();
        }

        // if track is stopped, play it
        if (playBtn.getAttribute("class") === "paused") {
          audioElement.play();
          playBtn.setAttribute("class", "playing");
          playBtn.textContent = "Pause";
          // if track is playing, stop it
        } else if (playBtn.getAttribute("class") === "playing") {
          audioElement.pause();
          playBtn.setAttribute("class", "paused");
          playBtn.textContent = "Play";
        }
      });

      // if track ends
      audioElement.addEventListener("ended", () => {
        playBtn.setAttribute("class", "paused");
        playBtn.textContent = "Play";
      });

      // volume
      const gainNode = audioCtx.createGain();

      volumeSlider.addEventListener("input", () => {
        gainNode.gain.value = volumeSlider.value;
      });

      // connect our graph
      audioSource.connect(gainNode).connect(audioCtx.destination);

      // Track credit: Outfoxing the Fox by Kevin MacLeod under Creative Commons
    </script>
  </body>
</html>
```
We start by creating an AudioContext instance inside which to manipulate our track: `const audioCtx = new AudioContext();` 

## Video and audio APIs

### The HTMLMediaElement API

> Part of the HTML spec, the HTMLMediaElement API provides features to allow you to control video and audio players programmatically — for example `HTMLMediaElement.play()`, `HTMLMediaElement.pause()`, etc. This interface is available to both `<audio> ` and `<video>` elements

### Getting started 
‌

> To get started with this example, follow these steps:

> 1.Create a new directory on your hard drive called custom-video-player.

> 2.Create a new file inside it called index.html and fill it with the following content:

```html
<!DOCTYPE html>
<html lang="en-gb">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Video player example</title>
    <link rel="stylesheet" type="text/css" href="style.css" />
  </head>
  <body>
    <div class="player">
      <video controls>
        <source
          src="/shared-assets/videos/sintel-short.mp4"
          type="video/mp4" />
        <source
          src="/shared-assets/videos/sintel-short.webm"
          type="video/webm" />
      </video>
      <div class="controls">
        <button
          class="play"
          data-icon="P"
          aria-label="play pause toggle"></button>
        <button class="stop" data-icon="S" aria-label="stop"></button>
        <div class="timer">
          <div></div>
          <span aria-label="timer">00:00</span>
        </div>
        <button class="rwd" data-icon="B" aria-label="rewind"></button>
        <button class="fwd" data-icon="F" aria-label="fast forward"></button>
      </div>
    </div>
    <p>
      Sintel &copy; copyright Blender Foundation |
      <a href="https://studio.blender.org/films/sintel/"
        >studio.blender.org/films/sintel/</a
      >.
    </p>
    <script src="custom-player.js"></script>
  </body>
</html>
```
and write style.css :
```css
@font-face {
  font-family: "HeydingsControlsRegular";
  src: url("https://mdn.github.io/learning-area/javascript/apis/video-audio/finished/fonts/heydings_controls-webfont.eot");
  src:
    url("https://mdn.github.io/learning-area/javascript/apis/video-audio/finished/fonts/heydings_controls-webfont.eot?#iefix")
      format("embedded-opentype"),
    url("https://mdn.github.io/learning-area/javascript/apis/video-audio/finished/fonts/heydings_controls-webfont.woff")
      format("woff"),
    url("https://mdn.github.io/learning-area/javascript/apis/video-audio/finished/fonts/heydings_controls-webfont.ttf")
      format("truetype");
  font-weight: normal;
  font-style: normal;
}

video {
  border: 1px solid black;
}

p {
  position: absolute;
  top: 310px;
}

.player {
  position: absolute;
}

.controls {
  visibility: hidden;
  opacity: 0.5;
  width: 400px;
  border-radius: 10px;
  position: absolute;
  bottom: 20px;
  left: 50%;
  margin-left: -200px;
  background-color: black;
  box-shadow: 3px 3px 5px black;
  transition: 1s all;
  display: flex;
}

.player:hover .controls,
.player:focus-within .controls {
  opacity: 1;
}

button,
.controls {
  background: linear-gradient(to bottom, #222222, #666666);
}

button::before {
  font-family: HeydingsControlsRegular;
  font-size: 20px;
  position: relative;
  content: attr(data-icon);
  color: #aaaaaa;
  text-shadow: 1px 1px 0px black;
}

.play::before {
  font-size: 22px;
}

button,
.timer {
  height: 38px;
  line-height: 19px;
  box-shadow: inset 0 -5px 25px #0000004d;
  border-right: 1px solid #333333;
}

button {
  position: relative;
  border: 0;
  flex: 1;
  outline: none;
}

.play {
  border-radius: 10px 0 0 10px;
}

.fwd {
  border-radius: 0 10px 10px 0;
}

.timer {
  line-height: 38px;
  font-size: 10px;
  font-family: monospace;
  text-shadow: 1px 1px 0px black;
  color: white;
  flex: 5;
  position: relative;
}

.timer div {
  position: absolute;
  background-color: rgb(255 255 255 / 20%);
  left: 0;
  top: 0;
  width: 0;
  height: 38px;
  z-index: 2;
}

.timer span {
  position: absolute;
  z-index: 3;
  left: 19px;
}

button:hover,
button:focus {
  box-shadow: inset 1px 1px 2px black;
}

button:active {
  box-shadow: inset 3px 3px 2px black;
}

.active::before {
  color: red;
}
```
<img width="1455" height="694" alt="image" src="https://github.com/user-attachments/assets/563e05bd-b429-4157-8e3b-4393e01708cf" />

> 4.Create another new file in the directory called custom-player.js. Leave it blank for now.

### Implementing the JavaScript
We've got a fairly complete HTML and CSS interface already; now we just need to wire up all the buttons to get the controls working.
<br>
1.At the top of the custom-player.js file, insert the following code:


```js
const media = document.querySelector("video");
const controls = document.querySelector(".controls");

const play = document.querySelector(".play");
const stop = document.querySelector(".stop");
const rwd = document.querySelector(".rwd");
const fwd = document.querySelector(".fwd");

const timerWrapper = document.querySelector(".timer");
const timer = document.querySelector(".timer span");
const timerBar = document.querySelector(".timer div");
```
2.Next, insert the following at the bottom of your code:


```
media.removeAttribute("controls");
controls.style.visibility = "visible";
```
These two lines remove the default browser controls from the video, and make the custom controls visible.

### Playing and pausing the video
1.First of all, add the following to the bottom of your code, so that the playPauseMedia() function is invoked when the play button is clicked:

``` play.addEventListener("click", playPauseMedia);```
2. Now to define playPauseMedia() — add the following, again at the bottom of your code:

```js
function playPauseMedia() {
  if (media.paused) {
    play.setAttribute("data-icon", "u");
    media.play();
  } else {
    play.setAttribute("data-icon", "P");
    media.pause();
  }
}
```
### Stopping the video

1.Next, let's add functionality to handle stopping the video. Add the following addEventListener() lines below the previous one you added:

```
stop.addEventListener("click", stopMedia);
media.addEventListener("ended", stopMedia);
```
The click event is obvious — we want to stop the video by running our stopMedia() function when the stop button is clicked. We do however also want to stop the video when it finishes playing — this is marked by the ended event firing, so we also set up a listener to run the function on that event firing too.

2. Next, let's define stopMedia() — add the following function below playPauseMedia():


```
function stopMedia() {
  media.pause();
  media.currentTime = 0;
  play.setAttribute("data-icon", "P");
}
```

## Drawing graphics
https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Client-side_APIs/Drawing_graphics

# What are third party APIs?
> Third party APIs are APIs provided by third parties — generally companies such as Facebook, Twitter, or Google — to allow you to access their functionality via JavaScript and use it on your site. One of the most obvious examples is using mapping APIs to display custom maps on your pages.

## They are found on third-party servers

To access them from JavaScript you first need to connect to the API functionality and make it available on your page

```html
<script
  src="https://api.mqcdn.com/sdk/mapquest-js/v1.3.2/mapquest.js"
  defer></script>
<link
  rel="stylesheet"
  href="https://api.mqcdn.com/sdk/mapquest-js/v1.3.2/mapquest.css" />
```
You can then start using the objects available in that library. For example:

```js
const map = L.mapquest.map("map", {
  center: [53.480759, -2.242631],
  layers: L.mapquest.tileLayer("map"),
  zoom: 12,
});
```
> Here we are creating a variable to store the map information in, then creating a new map using the mapquest.map() method, which takes as its parameters the ID of a <div> element you want to display the map in ('map'), and an options object containing the details of the particular map we want to display. In this case we specify the coordinates of the center of the map, a map layer of type map to show (created using the mapquest.tileLayer() method), and the default zoom level.
> This is all the information the Mapquest API needs to plot a simple map. The server you are connecting to handles all the complicated stuff, like displaying the correct map tiles for the area being shown, etc.


## They usually require API keys
Security for browser APIs

## Mapquest example
```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mapquest example</title>
    <script src="https://api.mqcdn.com/sdk/mapquest-js/v1.3.2/mapquest.js" defer></script>
    <script src="script.js" defer></script>
    <link type="text/css" rel="stylesheet" href="https://api.mqcdn.com/sdk/mapquest-js/v1.3.2/mapquest.css"/>
    <link href="style.css" rel="stylesheet">
  </head>
  <body>
    <h1>Simple Mapquest example</h1>

    <div id="map"></div>
  </body>
</html>
```

style: 
```
#map {
  width: 600px;
  height: 600px;
}
```
index.js:
```L.mapquest.key = 'YOUR-API-KEY-HERE';

// 'map' refers to a <div> element with the ID map
const map = L.mapquest.map('map', {
  center: [53.480759, -2.242631],
  layers: L.mapquest.tileLayer('map'),
  zoom: 12
});
```

> Next, you need to go to the Mapquest developer site, create an account, and then create a developer key to use with your example. (At the time of writing, it was called a "consumer key" on the site, and the key creation process also asked for an optional "callback URL". You don't need to fill in a URL here: just leave it blank.)
> Open up your starting file, and replace the API key placeholder with your key

## costomize
<a href="https://developer.mapquest.com/documentation/sdks/mapquest-js/l-mapquest-map.html"> for more information rea documents </a>

# piblic api list 
<a href="https://github.com/public-apis/public-apis"> click me</a>

# Building your own api
> Monetised apis
> > data calection
> > algorithm service
> > simplified interface

## using GET method for a example
 <a href=" https://documenter.getpostman.com/view/6048123/2s9XxsTv8Y
"> joke Api</a>


































