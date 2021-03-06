# Install
### Full development environment install
[Full install guide](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/dev-env-setup/)

[Prerequisites](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/dev-env-setup/)
[Start UI from Set-Up-Box](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/start-ui/)
[Debugging](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/debug-testing/) : both on browser and remotely on STB embedded webkit browser
[REST-console ](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/call-rest-api/) : to test request to server

### Install on local computer
-  @feb 2017, no STB is installed, so we only use a computer running Linux, a browser and node

- download code

```
$ git clone git@github.com:frogbywyplay/apps_frog-ui.git
```

(prerequisite : open github account and access to source - ssh key)

- Install node and npm
```
$ sudo apt-get update
$ sudo apt-get install nodejs
$ sudo apt-get install npm
```

/!\ to resolve conflicting "node" use
```
$ sudo ln -s /usr/bin/nodejs /usr/local/bin/node
```
- cf. README from code :
Install node local environment 
```
$ npm install
```

Start the webpack-dev-server :

	$ npm start

Open the UI in your browser using the following URL: [http://0.0.0.0:8080/?stbIp=127.0.0.1&debug=true](http://0.0.0.0:8080/?stbIp=127.0.0.1&debug=true)

Live reload works great. Every change in ./src is recompliled and browser is reloaded automatically
See README for all available options or read [here](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/start-ui/) 

- debug=true exposes main helpers (e.g : bus) in Chrome debug console
- Default setup are listed here "config.json". For project set-up, duplicate and rename "config.json" to "config.local.json". For quick/debug set-up on the fly, change query search options in the URL (flags need to be defined in app/config/index.js)

# Code
### Directory tree
Including brief description and doc links

**RootDirectory**
>
.
├── doc : *script to generate documentation*
├── script : *other scripts (e.g cli output)*
├── src : *ui js script*
├── test : *unit test code*
├── CHANGELOG : *log changes in different versions of code*
├── config.json : *default config, to be overrided by config.local.json*
├── config.webpack.json : *config for webpack server*
├── CONTRIBUTING.md
├── LICENSE
├── package.json : *list modules dependencies and available script*
├── README.md
└── webpack.config.babel.js : *config for module bundling*


**Javascript sources**
>
./src
├── app
├── locales : 
├── [services](#services)
├── [utils](#utils)
├── widgets
├── index.css
├── index.html
└── index.js

**App** : interface interaction, interface intelligence
>
./src/app
├── assets
├── components > DOM ecapsulated in js files
├── config
├── controllers
├── models
└── utils

**Services**<a name="services"></a> : business intelligence
>
./src/services
├── api
│   ├── index.js
│   ├── scan.js
│   └── ...
├── managers
│   ├── index.js
│   ├── ScanManager.js
│   ├── UniverseManager.js : initialize App controllers
│   ├── volume.js
│   └── ...
├── models
│   ├── channels
│   ├── ...
│   ├── index.js
│   ├── Subtitle.js
│   └── ...
├── [bus.js](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/api-bus/)
├── [events.js](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/api-events/) 
├── [http.js](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/api-http/)
└── Model.js


/!\ Portal Frog documentation is outdated

Widgets : Graphic helpers
>
./src/widgets
├── list
├── [Component.js](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/Component/)
└── index.js

Code concept, architecture and philosophy follows [JSX](https://jsx.github.io/) and [BEM](http://blog.kaelig.fr/post/48196348743/fifty-shades-of-bem)

Utils<a name="utils"></a>
[Link to doc]((https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/utils/))
>
./src/utils
├── CircularList.js
├── config.js
├── [Controller.js](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/api-Controller/) 
├── date.js
├── dom.js
├── Singleton.js
├── string.js
└── ...

### Code documentation
##### Generate documentation
In project root :

```
$ npm run build-doc
```
Documentation will build here : [apps_frog-ui/esdoc/index.html]

##### Comments

- /!\ HelloWorld tutorial is outdated. It does not match current code.
- 10% functions are commented 
- *Class*, *Functions* and *Variables* are listed here : [apps_frog-ui/esdoc/identifiers.html]

- *API webservices* are listed here : [apps_frog-ui/esdoc/source.html]

	(eg : volume.js service disposes of following webservices and REST calls : decreaseVolume, increaseVolume, getMute, mute, unmute)

- Implemented unit tests : [apps_frog-ui/esdoc/test.html]

- /!\ mocking request to API can be done using JS library [xhr-mock](https://github.com/jameslnewell/xhr-mock). List of all routes used in the frog-ui along with request and response samples are available [here](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/wyrest/http/routes/) 


# HelloWorld 
### Code

	$ git clone git@gitlab.td.lan:randrianaivoe1/frog-ui.git
	
### Overview
![](./hello_world.png) 

### Feature
- display a new component when pressing OK from the remote/keyboard on the "helloworld" menu item (follow step a, b and c)
- display data by calling REST Api (cf. src/app/controllers/HelloWorld/index.js)
- display data SENT by the MiddleWare (cf. src/app/controllers/HelloWorld/index.js)

### Steps
##### a. Create Component
component : DOM unit used by the application to define both UI component (example : a button)and views (example: a side-bar)

	$ mkdir src/app/components/universes/HelloWorld
	$ touch src/app/components/universes/HelloWorld/index.js


style component

	$ touch src/app/components/universes/HelloWorld/index.css

add component to the "Application" main view defined in : src/app/components/index.js

- import component
- add component to DOM tree

##### b. Create Controller
controller : listens to events (from MW, from Application via Bus, from Keyboard), update view, retrieve via service API

	$ mkdir src/app/controllers/HelloWorld/
	$ touch src/app/controllers/HelloWorld/index.js

controller needs to be referenced in main Manager defined in : src/app/services/managers/UniverseManager.js

##### c. Add to Menu
add "Hello World" item to Home Menu in : src/app/models/Home.js


# Feedback

- on-trend technologie, ahead of time (ES6, css-next)
- modular code
- maintainable code with coding rules (cf. file .eslintrc)
- MVC
- HelloWorld required some retro-engineering since code structure and architecture changed from what is documented

>**Conclusion : **
> code is generic enough, as well as documented and structured. Existing features works as good examples to developnew features.
> Adding new components using existing features is possible
> To pick up on the code, knowledge of Babel ES6 and webpack or likewise libraries is required

# Glossary
#### Technologies
Nodejs, npm, Javascript, HTML, CSS
[Babel](http://babeljs.io/) : Javascript compiler - allows the use of ECMAScript 6 [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript). Compiler targets ECMAScript ES5 (supported by most browsers)
[Mocha](https://mochajs.org/) : unit test framework - handles async calls
[webpack](https://webpack.github.io/docs/what-is-webpack.html) : module bundler, build code in unique file main.js 

#### Libraries

Library | Description
--- | --- 
css-loader, exports-loader, json-loader, style-loader, file-loader | chaque loader prend un fichier source et retourne la nouvelle source après la moulinette webpack
[eslint](https://www.npmjs.com/package/eslint) | JS lint*
[stylelint](https://www.npmjs.com/package/stylelint) | CSS lint*
[xhr-mock](https://github.com/jameslnewell/xhr-mock) | mock response to server request
[istanbul](https://github.com/gotwarlost/istanbul) | code coverage - Mocha dependency
[jsdom](https://github.com/tmpvar/jsdom) | mock DOM using JS - Mocha dependency
[postcss](http://postcss.org/) | compil [Css-next](http://cssnext.io/) (CSS form the future) in compatible CSS
[mixin](https://www.npmjs.com/package/mixin-js) | JS object tools
[array-flatten](https://github.com/blakeembrey/array-flatten) |  array tool
[sinon](https://www.npmjs.com/package/sinon) | test spies, stubs and mocks.

*lint : code checker (common mistakes, respect coding standards, codes rules)


