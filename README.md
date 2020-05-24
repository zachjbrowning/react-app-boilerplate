# React App Boilerplate

## Description
A good starting point for creating a react app! It uses - 
 - ⚛️ React (DUHH) for the frontend
 - 🎒 Webpack to bundle up all your modules
 - 🔏 Babel to compile all your javascript
 - ⏩ Express for a minimal backend

## Webpack things

### Loaders
Loaders are included and should work straight away for js, html, css and any static files. Trying to asynchronously require files in React can cause a bit of an issue though, read more in the section on asynchronous file loading.

### Bundling and splitting
Webpack has been used to split up bundles. The chunknames are hashed so that any cached files are updated when changed. To aid the splitting, I would really reccomend using react-loadable as a way to lazy load and split up any chunks that can be. 

### The issue of asynchronous file loading
Some of the work I have been doing includes creating react apps from a json file. This means that when an image is loaded, the source of the file is never written in plaintext in a react element. This makes things difficult in production mode for webpack loading the files into the dist folder. Having hashed chunks makes this problem even more difficult. My solution to this issue (and please let me know if you know of a more elegant one!!) is to move the unhashed necessary files to the dist folder before running the server. This can be done by running the dist script, which will copy over the contents of the public folder to dist, and files can then be accesed at /public/PATH_TO_FILE. 

This may mean that any files that are succesfully hashed and loaded have duplicates in dist (pretty much any files directly embedded in React JS components). If this is an issue, I would reccomend using two seperate folders - one for the embedded files and the public one for asynchronously loaded ones. This way the embedded files will be hashed and succesfully loaded and the public ones will just be copied over. Where they are asynchronously loaded, don't use import or require to avoid them being hashed and loaded, just use src='public/PATH_TO_FILE' directly in the element.

## Express things

Currently the backend is just about as minimal as it gets. Inside server/index.js you will see that all there is is an open regex that collects all the urls and redirect them to the entry point of the app. This is purposely done as this boilerplate is aimed at frontend dev. I am yet to really dive into elegant js driven backend solutions, after having worked with React and Django (which I can tell you don't go together beautifully...)