---
title: "XKCD Explainer Button"
date: 2021-04-23
---
  
This project was just a little side-thing to learn how extensions.  
So how do extensions work? Extensions are basically just a little website that runs when you open a compatible page. I have mine set up to run ```xkcd.js``` when xkcd.com is open. This is a really simple script so I'll talk y'all through it. The full code is on [github](https://github.com/l3gacyb3ta/xkcd-explain-button).  

## The code

```
var navbar = document.getElementsByClassName("comicNav")[0];
```
This line is pretty cool, thanks Randall for making the navbar have it's own class name. This code just grabs the navbar and stores it in a variable. I'll probably make it use (```let``` instead of ```var```)[https://evertpot.com/javascript-let-const/] in a future release.  

```
var xkcdNum = window.location.href.split('/')[3];
```
This just gets the number of the current xkcd, or if you're on the latest one, just an empty string.  
```
var link = "https://explainxkcd.com/"+xkcdNum;
```
Here I generate the (explainxkcd)[https://explainxkcd.com] link for the comic number we got in the previous line. Just some concatination. (I love that word.)  
```
navbar.innerHTML = navbar.innerHTML + "<li><a href=\"" + link + "\"> Explain</a><li>"
```
This is pretty fun. The navbar is a ul so here I just add a list element (li) to the list that links to the link we make earlier. Now the script is done, but the extenioning is far from over.  
  
## The metadata
  
In order for this extension to work, it needs a manifest. Specifically a file called ```manifest.json```. This file will contain some info the browser need to work. Here's the first bit:  
```
"name": "XKCD Button Explainer",
"version": "1.0",
"description": "Adds an explain this button to xkcd",
"icons": {
"48": "icons/xkcd-48.png"
},
```  
This bit gives the name of the extension, the version number (which I haven't ever changed), and a little description. The next bit just links to some creative commons icon I found from Google. This bit was pretty simple so lets get onto the cool stuff!
```
"content_scripts": [
{
    "matches": ["*://*.xkcd.com/*"],
    "js": ["xkcd.js"]
}
]
```
This little bit explains to the browser that, when the URL matches the pattern ```"*://*.xkcd.com/*"```. That pattern tells the browser that when I'm on xkcd.com, any of it's subdomains, and on any protocol, to run the js file ```xkcd.js```. ```xkcd.js``` which is the script I explained earlier.  

## Wrap-up
That's the scoop on how extentions work, they're supprisingly simple! This was a really fun project, even though it's only really 4 lines of code that could be one line. So thanks for following along, and I will see you on the interwebs!  
  
-l3gacy