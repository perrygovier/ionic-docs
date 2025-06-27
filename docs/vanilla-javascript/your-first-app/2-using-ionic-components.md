---
sidebar_label: Using Iconic Components
---

# Using Ionic Components in Vanilla JavaScript

## Add Ionic Tabs

Ionic’s `ion-tabs` component lets you build tabbed navigation similar to what you’d find in a mobile music or podcast app. In this section, we’ll add a basic tab layout to your project using just HTML.

We’ll be using the **Basic Usage** example from the [Tabs component documentation](../../api/tabs), and modifying it slightly to work in our Vanilla JavaScript project.

---

### 1. Insert Tabs Markup

Copy the following HTML and paste it inside the `<body>` element of your `index.html` file. This creates four tabs: **Listen Now**, **Radio**, **Library**, and **Search**.

:::note
You only need the HTML portion — you can ignore the `.ts` example shown in the documentation.
:::

```html
<ion-tabs>
  <ion-tab tab="home">
    <div id="home-page">
      <ion-header>
        <ion-toolbar>
          <ion-title>Listen now</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <div class="example-content">Listen now content</div>
      </ion-content>
    </div>
  </ion-tab>

  <ion-tab tab="radio">
    <div id="radio-page">
      <ion-header>
        <ion-toolbar>
          <ion-title>Radio</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <div class="example-content">Radio content</div>
      </ion-content>
    </div>
  </ion-tab>

  <ion-tab tab="library">
    <div id="library-page">
      <ion-header>
        <ion-toolbar>
          <ion-title>Library</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <div class="example-content">Library content</div>
      </ion-content>
    </div>
  </ion-tab>

  <ion-tab tab="search">
    <div id="search-page">
      <ion-header>
        <ion-toolbar>
          <ion-title>Search</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <div class="example-content">Search content</div>
      </ion-content>
    </div>
  </ion-tab>

  <ion-tab-bar slot="bottom">
    <ion-tab-button tab="home">
      <ion-icon name="play-circle"></ion-icon>
      Listen Now
    </ion-tab-button>

    <ion-tab-button tab="radio">
      <ion-icon name="radio"></ion-icon>
      Radio
    </ion-tab-button>

    <ion-tab-button tab="library">
      <ion-icon name="library"></ion-icon>
      Library
    </ion-tab-button>

    <ion-tab-button tab="search">
      <ion-icon name="search"></ion-icon>
      Search
    </ion-tab-button>
  </ion-tab-bar>
</ion-tabs>
```

Our application should now appear something like this:

![Screenshot of the application at this point in development](https://i.imgur.com/Cf0AcXu.png)

---

### 2. Modify the Radio Elements

Next, we’ll replace the **Radio** tab with a **Gallery** tab to better suit our photo app.

Update your HTML by replacing the existing Radio tab markup with this:

```html 
<!-- <ion-tabs>... -->
<ion-tab tab="gallery">
  <div id="gallery-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Gallery</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <div class="example-content">Gallery content</div>
    </ion-content>
  </div>
</ion-tab>
```

Then, update the corresponding tab button inside the tab bar to:
```html
<!-- <ion-tab-bar slot="bottom">... -->
<ion-tab-button tab="gallery">
  <ion-icon name="images"></ion-icon>
  Gallery
</ion-tab-button>
```

Your application should now display **Gallery** in place of **Radio**.
![Screenshot of the application at this point in development](https://i.imgur.com/OGC3nbn.png)

## Page Layouts

To build responsive layouts in Ionic, we’ll use the [`ion-grid`](/docs/api/grid), [`ion-row`](/docs/api/row), and [`ion-col`](/docs/api/col) components. These help us structure the content of our app so it displays well across all screen sizes.

We’ll now update the Gallery tab to include these layout elements. We'll build the structure step by step.

---

### 1. Add `ion-grid`

The `ion-grid` acts as the main container for rows and columns. It uses a flex-based layout system and supports responsive breakpoints.

Update your Gallery tab to include a grid inside the `<ion-content>`:

```html
<ion-content>
  <ion-grid>
    ...
  </ion-grid>
</ion-content>
```

### 2. Add `ion-row`
Inside the grid, we use an `ion-row` to organize horizontal sections. This acts like a flex row and wraps ion-col elements.

Add a single row within your grid:
```html
<ion-grid>
  <ion-row>
    ...
  </ion-row>
</ion-grid>
```

### 3. Add `ion-col` for Layout Sections
Within each row, use `ion-col` to define individual columns. Columns are responsive by default and will automatically stack on smaller screens.

For our layout, we’ll use two columns:

**Camera Column**
```html
<!-- Camera Column -->
<ion-col size="12" size-md="6">
  ...
</ion-col>
```

**Gallery Column**
```html
<!-- Gallery Column -->
<ion-col size="12" size-md="6">
  ...
</ion-col>
```

#### Full Layout Example
Once you’ve added all the elements, your `Gallery` tab should now look like this:
```html
<ion-tab tab="gallery">
  <div id="gallery-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Gallery</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-grid>
        <ion-row>
          <!-- Camera Column -->
          <ion-col size="12" size-md="6">
            ...
          </ion-col>

          <!-- Gallery Column -->
          <ion-col size="12" size-md="6">
            ...
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </div>
</ion-tab>
```

#### Lets Get Visual
To help understand this concept, below is an image with each of these elements added, with CSS borders around each element:
- Purple: `ion-grid`
- Red: `ion-row`
- Blue: `ion-col`
![Demonstration of Element Borders](https://i.imgur.com/bqOsPpd.png)

## Smile! Adding a Camera

Let’s start setting up the **Camera Column** of our app. This is where we’ll display a live video preview from your device’s camera and eventually capture photos.

### 1. Create a Camera Frame

We’ll begin by creating a wrapper `<div>` that will hold our camera feed. Inside that wrapper, we’ll add a `<video>` element that will stream the live camera preview.

Open your `index.html` and inside the **Camera Column’s** `<ion-col>`, add the following:

```html
<!-- Camera Column -->
<ion-col size="12" size-md="6">
  <div class="video-container">
    <video id="video"></video>
    ...
  </div>
</ion-col>
```

Here’s what each part does:

- `<div class="video-container">`: Acts as a frame for the camera view. *This has already been styled with CSS to control its size and layout.*

- `<video id="video">`: This element will display the live feed from the user’s camera!

At this point, we should be able to **see** some progress!
![Screenshot of the application at this point in development](https://i.imgur.com/QKdY8dc.png)

### 2. Add a Camera Button with `ion-fab`
Now let's place a button on top of the video feed so users can take a photo. We'll use [`ion-fab`](../../api/fab), Ionic's floating action button component, to do this.

Inside the same `video-container` div, right after the `<video>` element, add:
```html
<ion-fab class="fab-inside-video">
  <ion-fab-button id="start-button">
    <ion-icon name="camera"></ion-icon>
  </ion-fab-button>
</ion-fab>
```

- [`ion-fab`](../../api/fab) positions the button, floating over the video.
- `ion-fab-button` creates a native-looking action button.
- Inside `ion-fab-button`, we're using an [`ion-icon`](../../api/icon) with the `camera` icon to visually indicate the action.

**Current Code Sample:**
```html
<ion-content>
  <ion-grid>
    <ion-row>
      <!-- Camera Column -->
      <ion-col size="12" size-md="6">
        <div class="video-container">
          <video id="video"></video>
          <ion-fab class="fab-inside-video">
            <ion-fab-button id="start-button">
              <ion-icon name="camera"></ion-icon>
            </ion-fab-button>
          </ion-fab>
        </div>
      </ion-col>

      <!-- Gallery Column -->
      <ion-col size="12" size-md="6">
        ...
      </ion-col>
    </ion-row>
  </ion-grid>
</ion-content>
```

**And our app should look like this!**
![Screenshot of the application at this point in development](https://i.imgur.com/lbVrvD4.png)


## Photo Gallery

Let’s build out the **Gallery Column** where the photos will appear after they're taken. Ionic’s Grid system makes it easy to display items in a clean, responsive layout.

Our app will use a combination of `ion-grid`, `ion-row`, and [`ion-image`](../../api/img) to show photos as they are captured. We’ll be dynamically inserting the images with JavaScript, but here’s how to set up the layout.

### 1. Add  an `ion-grid`

Inside the **Gallery Column’s** `<ion-col>`, add an `ion-grid`. This sets up a responsive container for your image layout.

```html
<!-- Gallery Column -->
<ion-col size="12" size-md="6">
  <ion-grid class="gallery-scroll">
    ...
  </ion-grid>
</ion-col>
```

### 2. Add an `ion-row` for Image Output
Now inside of that `ion-grid`, add an `ion-row` where we'll place each photo. Our `demo.js` file will insert new [`ion-image`](../../api/img) elements inside this row as photos are taken.

```html
<ion-row id="photo-row" class="output"></ion-row>
```

**Current Code Sample:**
```html
<ion-content>
    <ion-grid>
        <ion-row>
            <!-- Camera Column -->
            <ion-col size="12" size-md="6">
                <div class="video-container">
                <video id="video"></video>
                <ion-fab class="fab-inside-video">
                    <ion-fab-button id="start-button">
                    <ion-icon name="camera"></ion-icon>
                    </ion-fab-button>
                </ion-fab>
                </div>
            </ion-col>

            <!-- Gallery Column -->
            <ion-col size="12" size-md="6">
                <ion-grid class="gallery-scroll">
                    <ion-row id="photo-row" class="output"></ion-row>
                </ion-grid>
            </ion-col>
        </ion-row>
    </ion-grid>
</ion-content>
```

#### Say Cheese!
At this point, we should now have a completed app. #selfie!
![Screenshot of the completed application](https://i.imgur.com/jr36PWV.jpeg)



