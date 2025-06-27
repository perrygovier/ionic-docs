---
sidebar_label: Build Your First App
---

# Your First Ionic App: Vanilla JavaScript

The great thing about Ionic is that with one codebase, you can build for any platform using just HTML, CSS, and JavaScript. Follow along as we learn the fundamentals of Ionic app development by creating a realistic app step by step.

Here's the finished app running on all three platforms:
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/ZA7ZKB8Mo9k"
  frameBorder="0"
  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
  allowFullScreen
></iframe>

## What We'll Build
We'll create a Photo Gallery app that offerrs the ability to take photos with your device's camera and display them in a grid.

You can find the **complete app code** referenced in this guide [on GitHub](https://github.com/kkindrai/Ionic--VanillaJS-Getting-Started-Application)

## Download Required Tools
Download and install these right away to ensure an optimal Ionic development experience:

- **A code editor** for... writing code! We are fans of [Visual Studio Code](https://code.visualstudio.com/).

## Create Your Working Directory

Before you start building your app, you'll need to set up a folder where all your project files will live. This includes creating an HTML file and generating the basic structure of a webpage using VS Code.

### 1. Create a new project folder

Start by creating a new folder on your computer. You can name it anything you like — for example, `my-ionic-app`.

To do this:

- Open your computer’s file manager (Finder on macOS, File Explorer on Windows)
- Navigate to where you want your project to be saved (like your Desktop or Documents folder)
- Right-click and choose **New Folder**
- Name the folder something like `my-ionic-app`

### 2. Add a blank `index.html` file

Next, create a new file inside your folder called `index.html`.

To do this:

- Open the folder you just created
- Right-click inside the folder and choose **New File** (or **Text Document**, then rename it)
- Name the file `index.html` — make sure the extension is `.html`, not `.txt`

> **Note:** If you don’t see the file extension, you may need to enable “Show file extensions” in your system settings.

### 3. Generate the base HTML template

Now, open the folder in [Visual Studio Code](https://code.visualstudio.com/), and open the `index.html` file.

In the editor:

1. Click inside the file  
2. Type `!` and press `Tab`  
3. VS Code will automatically expand it into a full HTML5 document structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      
  </body>
</html>
```

> **Tip:** If `! + Tab` doesn’t work, make sure the file is saved as `index.html`, and that your cursor is inside the file.

## Import Ionic Scripts

To start using Ionic components in your app, you'll need to include the Ionic JavaScript and CSS files. These are loaded from a CDN (Content Delivery Network) and allow your project to access the full Ionic Core library.

### Add the Ionic scripts to your HTML file

Open your `index.html` file and locate the `<head>` section. Inside the `<head>`, directly below the `<title>` tag, paste the following lines:

```html
<!-- Import Ionic Scripts -->
<script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
<script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
```

After adding the scripts, your file should look like this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <!-- Import Ionic Scripts -->
    <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
    <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
  </head>
  <body>
    
  </body>
</html>
```

> **Note:** These scripts load Ionic Core in a way that works with most modern browsers. The `type="module"` version is used for browsers that support JavaScript modules, while the `nomodule` fallback ensures compatibility with older browsers.


## Downloading App Specific Resources

In addition to the Ionic Core scripts, your app will use two custom files: a JavaScript file for functionality and a CSS file for styling.

### 1. Download the files

Download each of the following files and save them in the same folder as your `index.html` file:

- [View `demo.js`](https://raw.githubusercontent.com/kkindrai/Ionic--VanillaJS-Getting-Started-Application/main/demo.js)
- [View `styles.css`](https://raw.githubusercontent.com/kkindrai/Ionic--VanillaJS-Getting-Started-Application/main/styles.css)

> **Note:** Make sure both files are saved directly inside your project folder (next to `index.html`), not in a subfolder.

#### `demo.js` (click to expand)

<details>
<summary>View file contents</summary>

```js title="demo.js"
// Code Sample Modified from Mozilla
// https://developer.mozilla.org/en-US/docs/Web/API/Media_Capture_and_Streams_API/Taking_still_photos

// Global Variables
const gallery     = [];   // Array to store captured images
const size        = 320;  // Viewport Size
let   streaming   = false;
let   canvas      = null;
let   photoRow    = null;
let   startButton = null;
let   video       = null;

  
/**
 * Clears the canvas by filling it with a gray color.
 * This is used to reset the canvas before capturing a new image.
 */
function clearPhoto() {
  const context = canvas.getContext("2d");
  context.fillStyle = "#AAA";
  context.fillRect(0, 0, canvas.width, canvas.height);
}

/**
 * Renders the gallery of captured images.
 * It creates a grid layout using ion-col elements for each image.
 */
function renderGallery() {
  photoRow.innerHTML = "";
  gallery.forEach((imgUrl) => {
    const ionCol = document.createElement("ion-col");
    ionCol.setAttribute("size", "4");

    const ionImg = document.createElement("ion-img");
    ionImg.setAttribute("src", imgUrl);
    ionImg.style.width = "100%";
    ionImg.style.height = "auto";
    ionImg.style.margin = "4px";

    ionCol.appendChild(ionImg);
    photoRow.appendChild(ionCol);
  });
}


/**
 * Captures a picture from the video stream and adds it to the gallery.
 * The picture is centered and cropped to a square based on the video aspect ratio.
 */
function takePicture() {
  const context = canvas.getContext("2d");
  if (size) {
    canvas.width = size;
    canvas.height = size;

    // Center-crop the video to a square
    const videoAspect = video.videoWidth / video.videoHeight;
    let sx, sy, sWidth, sHeight;

    if (videoAspect > 1) {
      // Video is wider than tall
      sHeight = video.videoHeight;
      sWidth = sHeight;
      sx = (video.videoWidth - sWidth) / 2;
      sy = 0;
    } else {
      // Video is taller than wide or square
      sWidth = video.videoWidth;
      sHeight = sWidth;
      sx = 0;
      sy = (video.videoHeight - sHeight) / 2;
    }

    // Draw the video frame onto the canvas
    context.drawImage(
      video,
      sx, sy, sWidth, sHeight, // source rectangle
      0, 0, size, size         // destination rectangle
    );

    // Convert the canvas to a data URL and add it to the gallery
    const data = canvas.toDataURL("image/png");
    gallery.push(data);
    renderGallery();
  } else {
    clearPhoto();
  }
}

/**
 * Initializes the app by setting up the video stream and event listeners.
 */
function startup() {
  // Get references to the HTML elements
  video = document.getElementById("video");
  canvas = document.getElementById("canvas");
  startButton = document.getElementById("start-button");
  photoRow = document.getElementById("photo-row");

  // Check if the browser supports the MediaDevices API
  navigator.mediaDevices
    .getUserMedia({ video: true, audio: false })
    .then((stream) => {
      video.srcObject = stream;
      video.play();
    })
    .catch((err) => {
      console.error(`An error occurred: ${err}`);
    });

  // Set up event listeners for the video element
  video.addEventListener(
    "canplay",
    () => {
      if (!streaming) {
        video.setAttribute("width", size);
        video.setAttribute("height", size);
        canvas.setAttribute("width", size);
        canvas.setAttribute("height", size);
        streaming = true;
      }
    },
    false,
  );

  // Set up the start button to capture a picture
  startButton.addEventListener(
    "click",
    (ev) => {
      takePicture();
      ev.preventDefault();
    },
    false,
  );
  clearPhoto();
}

// Initialize the app when the window loads
window.addEventListener("load", startup, false);
```

</details>

#### `styles.css` (click to expand)

<details>
<summary>View file contents</summary>

```css title="styles.css"
ion-content {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    min-height: calc(100vh - 23vh); /* Ensure full window height minus nav bar */
}

ion-grid {
    height: 100%;
}

ion-row { 
    min-height: 100%;
    height: 100%; 
}

ion-col {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}

ion-grid.gallery-scroll ion-col {
    height: fit-content;
}

.gallery-scroll {
    overflow-y: auto;
    height: 100%;
}

.video-container {
    width: 75%;
    aspect-ratio: 1 / 1;
    height: auto; 
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
}

#video {
    width: 100%;
    height: auto;
    aspect-ratio: 1 / 1; 
    object-fit: cover;
    background: #000;
    display: block;
    border-radius: 8px; 
}

.fab-inside-video {
    margin-top: 75%;
    z-index: 2;
}

.hidden { 
    display: none;
}
```

</details>

### 2. Add local imports to your HTML file

Once the files are downloaded, import them into your project. Add the following lines directly below the Ionic import scripts inside your `<head>`:

```html
<!-- Import Local Scripts -->
<script src="demo.js"></script>
<link rel="stylesheet" href="styles.css" />
```

Your updated `<head>` section should now look like this:

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

  <!-- Import Ionic Scripts -->
  <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
  <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />

  <!-- Import Local Scripts -->
  <script src="demo.js"></script>
  <link rel="stylesheet" href="styles.css" />
</head>
```

### 3. Add the hidden canvas

At the very end of your `<body>` section, just before the closing `</body>` tag, add a hidden canvas element. This will be used later by the camera component:

```html
<!-- Hidden canvas -->
<canvas id="canvas" class="hidden"></canvas>
```

This canvas will remain invisible to users but will help process image data behind the scenes.


**This is what your `index.html` file should look like at the end of this step:**
```html title="index.html"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <!-- Import Ionic Scripts -->
    <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
    <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />

    <!-- Import Local Scripts -->
    <script src="demo.js"></script>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>

    <!-- Hidden canvas -->
    <canvas id="canvas" class="hidden"></canvas>
    
  </body>
</html>
```

