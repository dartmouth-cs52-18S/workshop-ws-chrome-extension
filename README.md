# CS52 Workshops: Chrome Extensions

![](http://i.giphy.com/eUh8NINbZf9Ys.gif)

Brief motivation here as well as in presentation

## Overview

Summary of what we're about to do.

## Setup

Any necessary setup steps

## Step by Step

### Create Manifest
* Create a ```manifest.json``` file in your directory.

```json
  {
    "manifest_version": 2,
    "name": "Chrome Exkittension",
    "version": "0.1",
    "content_scripts": [
        {
        "matches": [
          "<all_urls>"
        ],
        "js": ["kitten.js"]
      }
    ]
  }
```

Let's take a step back and examine what's going on here. Chrome extensions can have background scripts and/or content scripts. Background scripts run in the background and can be always running or can be idle and only run when triggered. Content scripts run in the context of the web page that you are currently on. By setting `matches` to `<all_urls>`, we are saying that we want our extension to run on all web pages. The `js` part of the manifest lists all of the javascript files that we will be using as part of the content script.

### Add some Javascript!
* Create a new file ```kitten.js```
* Add a ```console.log``` statement so we can ensure it's working.
```Javascript
  console.log('Where\'s Tim???');
```

### Link to Chrome Extensions
Now it's time to upload our extension to chrome!

* Go to [chrome://extensions](chrome://extensions) and make sure *Developer mode* in the upper right hand corner is toggled on.
![](readme_images/developer-mode.png)

* Click on *Load Unpacked* and select the directory that contains your chrome extension.

:white_check_mark: Check-in! Navigate to any [website](http://cs52.me/) and inspect the page. In the console, your previous ```console.log``` statement should now appear!

### Find image elements to replace
Let's take a moment to understand what we're looking for!
In the inspector console of the same page you just opened type
```javascript
  let imgs = document.getElementsByTagName('img');
```
Call ```imgs``` and open the HTMLCollection to view all the images on the page.
Expand any image number to view the attributes of the image. Scroll down until you see ```src``` (attributes should be alphabetical). We will be using the ```img``` tag to find and replace the source of each images with your own pictures!

Now you get to select your images! We have provided some default images in the img folder, but feel free to replace them with your own!

Whenever we have files inside the extension that we want to use (in this case, our pictures), we have to declare them inside ```manifest.json```.

Add the following in ```manifest.json``` before `content_scripts` :

```json
"web_accessible_resources": [
  "img/*.jpg",
  "img/*.jpeg"
],
```

This tells the manifest that we want the browser to be able to access these all of the jpeg images in the `img` folder. **If you are using different image formats (like pngs), make sure to include them in this part.**

We've played around in the inspector and understand what we are looking for. Let's code it up in our extension project.

We want to gather all of the images on the page into a variable, just like we did in the inspector. Add the following to `kitten.js`:

```javascript
  let imgs = document.getElementsByTagName('img');
```

We need an array containing the filenames of all of our images. Let's create that! Somewhere before you create the `imgs` variable, create a variable that references an array containing your image filenames:

```Javascript
let filenames = [
  "img/kitten1.jpg",
  "img/kitten2.jpg",
  "img/kitten2.jpg"
]
```

Now we have all the images of the website in a variable and an array holding all our image filenames. What do we need to do now?

If you said replace the current images with our own images, that's correct! We need a for-loop to loop through all of the current images. Let's just log the `src` of each image for now:

```Javascript
for (imgElt of imgs) {
  console.log(imgElt.src);
}
```

Now navigate back to [chrome://extensions](chrome://extensions) and hit refresh on the "Chrome Exkittension" extension:
![](readme_images/chrome_extension_refresh.png)

Navigate to any website (if you go to one that you already have opened make sure to refresh the page), and open up the inspector. You should see a list of the image sources!

But don't we want to replace the current images? Yep, we do! Instead of logging the image sources, let's set the source to a random filename from our array of filenames. Replace `console.log(imgElt.src);` with this:

```Javascript
  let r = Math.floor(Math.random() * filenames.length);
  let file = filenames[r];
  let url = chrome.runtime.getURL(file);
  imgElt.src = url;
  console.log(url);
```

What we are doing here is generating a random index into our array (the floor function makes sure that it is an integer), indexing into the array and grabbing that corresponding url, and setting the `src` of the image to that url. An interesting thing here is that we have to use `chrome.runtime.getURL`. We cannot just set `imgElt.src` equal to `file` because these files live inside our chrome extension and image sources need to be actual paths. `chrome.runtime.getURL` gives us back a valid URL of a file that is part of our chrome extension.

Reload the chrome extension and navigate to a webpage. All the images there should be replaced by yours!

# Tim's Instructions for README



* Explanations of the what **and** the why behind each step. Try to include:
  * higher level concepts
  * best practices

Remember to explain any notation you are using.

```javascript
/* and use code blocks for any code! */
```

![screen shots are helpful](img/screenshot.png)

:sunglasses: GitHub markdown files [support emoji notation](http://www.emoji-cheat-sheet.com/)

Here's a resource for [github markdown](https://guides.github.com/features/mastering-markdown/).


## Summary / What you Learned

* [ ] can be checkboxes

## Resources

* cite any resources
