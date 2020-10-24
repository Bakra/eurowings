# eurowings

Implement a simple web app that allows one to browse the Imgur gallery using https://api.imgur.com/:

show gallery images in a grid of thumbnails;
show image description in the thumbnail, top or bottom;
allow selecting the gallery section: hot, top, user;
allow including / excluding viralimages from the result set;
allow specifying windowand sort parameters;
it have lazy loading
when clicking an image in the gallery - show its details: big image, title, description, upvotes, downvotes and score.

## Project setup
### Note: If you have any issues, run it on node version 10
=> clone / setup the project on local machine
=> cd eurowings
=> yarn / npm install
=> yarn start (this will run express server and webpack server) or ( 'npm run serve' to start the frontend and 'node server.js' for express server).


### Compiles and hot-reloads for development

you can use yarn start or node server.js and yarn serve

### Compiles and minifies for production

```
npm run build
```

### Run your tests

```
npm run test
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
