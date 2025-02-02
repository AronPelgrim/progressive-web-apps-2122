# Art @ Home
<img width="100%" alt="Schermafbeelding 2022-03-08 144013" src="https://user-images.githubusercontent.com/74137185/157249410-7e098815-1f1e-48b4-8a09-6ca8c40cb6d5.png">

## Table of Contents

-   [About](#about)
-   [Live demo](#live-demo)
-   [Server side rendering](#server-side-rendering)
-   [User story](#user-story)
-   [Activity diagram](#activity-diagram)
-   [Critical render path](#critical-render-path)
-   [API](#api)
-   [How to install](#how-to-install)
-   [Wishlist](#wishlist)
-   [Any issues?](#any-issues)
-   [License](#license)

## About
Welcome to this repository. Here you can find my art app called **Art @ Home**. The concept is that the user can view art from the Rijksmuseum on their device. The user can look for their favourite artist and then the app will load in 5 paintings of that artist. If you click on the image, the user will arrive on the detail page, where they can view their favourite piece of art.

## Live demo
Follow this link to check out the full app!
[Art @ Home app](https://pwa-aron.herokuapp.com/)

## Server side rendering
I'm using server side rendering for this project. Server side rendering is the ability of an application to convert dynamic HTML files on the server into a fully rendered HTML page for the client. Because of server side rendering, the pages load faster, which improves the user experience. It also helps in efficiently loadinging web pages for users with slow connections to outdated devices. Also, server side rendering is good for SEO. Important content elements can be inspected directly without the pages having to render first.

## User story
>As an art lover, I want to be able to search and view art from the Rijksmuseum at home, so that I can still enjoy art during a lockdown. Despite of slow internet connection at home, I still want to be able to look at the paintings without waiting too long.

## Activity diagram
### Server
<img width="100%" alt="Schermafbeelding 2022-03-08 144013" src="https://user-images.githubusercontent.com/74137185/176659341-8b58a4a4-2379-4c30-9235-032bbca1b70d.png">

### Service worker
<img width="100%" alt="Schermafbeelding 2022-03-08 144013" src="https://user-images.githubusercontent.com/74137185/176688443-7fdefc1e-0440-4e5e-8c54-70d722265503.png">

## Critical render path
### Font-display: swap
I use this so that the browser is instructed to use the fallback font to display the text, until the custom font is completely downloaded.
```css
font-display: swap;
```

### Compression
Compression is used to reduce all files in size.
```javascript
const compression = require('compression')

app.use(compression())
```

### Caching headers
This can be used to control how caching can occur. This ensures that the request to the server does not have to be made all the time.
```javascript
let setCache = function (req, res, next) {
  const period = 60 * 5 

  if (req.method == 'GET') {
    res.set('Cache-control', `public, max-age=${period}`)
  } else {
    res.set('Cache-control', `no-store`)
  }
  next()
}
app.use(setCache)
```

### Minify
I have minified my CSS files by removing all unnecessary characters, to reduce the loading time.

## API
For this project, I'm using the Rijksdata API. To start using the data, you need to obtain an API key by registering for a [Rijksstudio account](https://www.rijksmuseum.nl/nl/registreer?redirectUrl=https://www.rijksmuseum.nl). You will be given a key instantly upon request, which you can find at the advanced settings of your Rijksstudio account. Some of the data elements that you can use from the API are the ```webImage``` to obtain the image, ```title``` for a short description, ```longTitle``` for a long description, ```principalOrFirstMaker``` for the name of the artist and ```id```, for the id of the painting.    

## How to install
### Clone this repo
```
$ git clone https://github.com/AronPelgrim/progressive-web-apps-2122.git
```

### Navigate to the repo
```
$ cd progressive-web-apps-2122
```

### Install necessary packages
``` 
$ npm install
```

### Start server
 ``` 
$ npm start 
 ```
Check it out! The server runs on localhost:3000.

## Wishlist
- [ ] A nicer error page.
- [ ] Do more with the serviceworker.
- [ ] Do more with the Critical Rendering Path.
- [ ] Being able to save a painting to user collection.

## Any issues?
You can create an issue in this repository to let me know what's wrong.

 ## License
[MIT](https://github.com/AronPelgrim/progressive-web-apps-2122/blob/main/LICENSE)