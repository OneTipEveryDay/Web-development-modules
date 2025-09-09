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

























































