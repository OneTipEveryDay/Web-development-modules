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
> 4.Create another new file in the directory called custom-player.js. Leave it blank for now.

























































