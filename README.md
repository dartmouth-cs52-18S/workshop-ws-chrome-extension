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

### Add some Javascript!
* Create a new file ```kitten.js```
* Add a ```console.log``` statement so we can ensure it's working.
```Javascript
  console.log('Where\'s Tim???');
```

### Link to Chrome Extensions
Now it's time to upload our extension to chrome!

* Go to [chrome://extensions](chrome://extensions) and make sure *Developer mode* in the upper right hand corner is toggled on.

* Click on *Load Unpacked* and select the directory that contains your chrome extension.

:white_check_mark: Check-in! Navigate to any [website](cs52.me) and inspect the page. In the console, your previous ```console.log``` statement should now appear!







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
