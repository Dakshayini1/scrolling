# Scrolling
### Hosted link: https://Dakshayini1.github.io/scrolling/

### Step 1: Create a New HTML File

Create a new HTML file and save it as `index.html`. Add the following code to your HTML file:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Endless Scroll</title>
    <link rel="stylesheet" href="style.css">
    <script defer src="index.js.js"></script>
</head>

<body>
    
    <h1>ENDLESS &nbsp; SCROLL</h1>

    
    <div class="loader" id="loader" >
        <img src="Spinner-1s-200px.svg" alt="laoding">
    </div>
    
    <div class="img-container" id="img-container">
    </div>
    
    <script>
        window.onload=function()
        {
        document.getElementById('loader').style.display='none'
    }
    </script>
</body>

</html>

```

### Step 2: Create a New CSS File

Create a new CSS file and save it as `style.css`. Add the following code to your CSS file:

```css
@import url('https://fonts.googleapis.com/css2?family=Dosis:wght@300&family=Sedgwick+Ave+Display&display=swap');

html {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Sedgwick Ave Display', cursive;
    background-color: whitesmoke;
}

h1 {
    text-align: center;
    margin-top: 25px;
    margin-bottom: 45px;
    font-size: 40px;
    letter-spacing: 1px;
    /* reflection */
    /* -webkit-box-reflect: below 0px linear-gradient(to bottom,rgba(0,0,0,0.0),rgba(0,0,0,0.4)); */
}

.loader {
    position: fixed;
    inset: 0;
    background: rgba(255, 255, 255, 0.8);
}

.loader img {
    position: fixed;
    top: 40%;
    left: 45%;
}

.img-container {
    margin: 10px 30%;
}

.img-container img {
    width: 100%;
    margin-top: 5px;
}

/* media query */

@media screen and (max-width:600px) {
    h1 {
        font-size: 20px;
    }
    .img-container {
        margin: 10px;
    }
}

```
### Step 3: Create a New js File

Create a new JS file and save it as `index.js`. Add the following code to your JS file:
```
const imageContainer = document.getElementById("img-container");
const loader = document.getElementById("loader");

let photosArray = [];

let ready = false;
let imagesLoaded = 0;
let totalImages = 0;

const count = 10;
const apikey = "_DDIVJSgdK-GI1wA3aHOtxC9YTt8tCY6-4jMk7guznY";
const apiUrl = `https://api.unsplash.com/photos/random/?client_id=${apikey}&count=${count}`;

function setAttribute(element, attributes) {
    for(const key in attributes) {
        element.setAttribute(key, attributes[key]);
    }
}

function imageLoaded() {
    imagesLoaded++;
    if(imagesLoaded === totalImages){
        ready = true;
        console.log("ready", ready);
    }
}

function displayPhotos() {
    totalImages = photosArray.length;

    imagesLoaded = 0;
    // for the next 10 images 

    photosArray.forEach((photo) => {
        const item = document.createElement("a");
        
        setAttribute(item, {
            href: photo.links.html,
            target: "_blank",
        });

        const img = document.createElement("img");
        setAttribute(img, {
            src: photo.urls.regular,
            alt: photo.alt_description,
            title: photo.alt_description,
        });

        img.addEventListener('load', imageLoaded);

        item.append(img);

        imageContainer.append(item);
    });
}


async function getPhotos() {
    try {
        const response = await fetch(apiUrl);
        photosArray = await response.json();
        displayPhotos();
    } catch (error) {
        console.log(error);
    }
}

window.addEventListener("scroll", () =>{
    if(window.scrollY + window.innerHeight >= document.body.offsetHeight && ready){
        ready = false;
        getPhotos();
    }
});

getPhotos();



```
