# tv-show-vuejs


> Vue.js application where you can see tv shows, search tvshows and seeing a tv show based on genre. When clicking you tv show you can see the detail page from this tv show.
This tv show application is made with the [TV MAZE API](https://www.tvmaze.com/api).

### Tech stack and architectural choices

TV-show-vuejs has the next technologie stack:

* VueJS- is a progressive framework for building user interfaces with javascript.
Vue.js is flexible and scalable. Has a lot of support and is future proof.Vue apps are smaller in size.
* SCSS - Sass is a CSS pre-processor
SCSS was implemented because it avoids to do repetive code. youocan put global variabel as it is also esay to mantain when making big changes with css.
* VueCLI: This is used to create the project and to install some basic dependencies. 
* ESlint: Checks the code in the editor for any mistakes or improvements. 
* BootstrapVue: UI library, with BootstrapVue you can build responsive, mobile-first. 
* Axios: HTTP client is widely used for its simplicity and options. It also automatically converts the response to JSON.

### What to improve
-Lazy loading will be a big plus regarding the bigger response you get back when searching a movie.
-Error habdeling with a nice page.
-Having the API requests in  singel file.


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
