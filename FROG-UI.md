## Lexique
####- Technologies
Nodejs, npm, Javascript, HTML, CSS
[Babel](http://babeljs.io/) : compilateur Javascript - permet d'écrire du JS en ECMAScript 6 [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)  et le compiler en cible ECMAScript ES5 (actuellement supporté sur tous les navigateurs)
[Mocha](https://mochajs.org/) : framework pour écrire des tests unitaires - permet de tester les appels asynchrones


####- Librairies :

Librairie | Descriptif 
--- | --- 
[webpack](https://webpack.github.io/docs/what-is-webpack.html) | module bundler, permet de builder tout le code et en sortir le main.js 
css-loader, exports-loader, json-loader, style-loader, file-loader | chaque loader prend un fichier source et retourne la nouvelle source après la moulinette webpack
[eslint](https://www.npmjs.com/package/eslint) | lint* pour le JS
[stylelint](https://www.npmjs.com/package/stylelint) | lint* pour le CSS
[xhr-mock](https://github.com/jameslnewell/xhr-mock) | mock response to server request
[istanbul](https://github.com/gotwarlost/istanbul) | code coverage - dépendence de Mocha
[jsdom](https://github.com/tmpvar/jsdom) | le DOM mocké en JS - dépendance de Mocha
[postcss](http://postcss.org/) | compile en JS [Css-next](http://cssnext.io/) (le CSS du futur) en CSS compatible
[mixin](https://www.npmjs.com/package/mixin-js) | outil pour les objets en Js
[array-flatten](https://github.com/blakeembrey/array-flatten) |  outils pour les tableaux
[sinon](https://www.npmjs.com/package/sinon) | test spies, stubs and mocks.

*lint : code checker (common mistakes, respect coding standards, codes rules)

## Étapes d'installation du code :
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
- suivre le README du code :
Installer l'environnement de développement web :
```
$ npm install
```

Démarrer un serveur local :

	$ npm start

Ouvrir l'UI ici : [http://0.0.0.0:8080/?stbIp=127.0.0.1&debug=true](http://0.0.0.0:8080/?stbIp=127.0.0.1&debug=true)  (Ref. README pour les options disponibles)

Les changements dans ./src sont bien prises en compte et le navigateur est rechargé automatiquement.

Une fois l'UI intégré à la STB, le remote debugging se fait selon la doc [ici](https://portal.frogbywyplay.com/docs/wytv/featured/guide-webapp-dev/debug-testing/).

N.B :

- debug=true, expose les helpers (e.g : bus) dans la console du navigateur
- Dupliquer le fichier "config.json" et renommer en "config.local.json" pour modifier les configurations, entrer l'IP de la setup-box


## L'arborescence du code avec bref descriptif

RootDirectory

	.
	├── CHANGELOG > log changes in different versions of code
	├── config.json > default config, to be overrided by config.local.json
	├── config.webpack.json > config for webpack server
	├── CONTRIBUTING.md
	├── doc > script to generate documentation
	├── LICENSE
	├── package.json > list modules dependencies and available script
	├── README.md
	├── script > other scripts (e.g cli output)
	├── src > ui js script
	├── test > unit test code
	└── webpack.config.babel.js > config for module bundling


Javascript Source

.
├── app
│   ├── assets
│   │   ├── ...
│   ├── components
│   │   ├── globals.css
│   │   ├── index.css
│   │   ├── ==index.js==
│   │   ├── universes
│   │   │   ├── Home
│   │   │   ├── ==HelloWorld==
│   │   │   │   ├── ==index.css==
│   │   │   │   └── ==index.js==
│   │   │   ├── PVR
│   │   │   ├── Television
│   │   │   └── ...
│   │   └── widgets
│   │       ├── Spinner
│   │       └── ...
│   ├── config
│   │   ├── alphanetworks.json
│   │   ├── index.js
│   │   └── keys
│   │       ├── defaultRCU.js
│   │       └── ...
│   ├── controllers
│   │   ├── EpgGrid
│   │   │   ├── EpgDetails.js
│   │   │   └── index.js
│   │   ├── Home
│   │   │   └── index.js
│   │   ├── ==HelloWorld==
│   │   │   └── ==index.js==
│   │   ├── PVR
│   │   │   ├── ...
│   │   ├── Television
│   │   │   ├── ChannelList.js
│   │   │   ├── index.js
│   │   │   ├── InfoBanner.js
│   │   │   ├── ProgramDetails.js
│   │   │   ├── ProgramList.js
│   │   │   └── Timeshift.js
│   │   └── ...
│   ├── models
│   │   ├──== Home.js==
│   │   └── Settings.js
│   └── utils
│       ├── epg.js
│       ├── locale.js
│       ├── PopUpMsg.js
│       └── widgets
│           └── lists.js
├── index.css
├── index.html
├── index.js
├── locales
│   ├── index.js
│   ├── manual
│   │   ├── category.pot
│   │   └── ...
│   └── po
│       ├── locale-en_EN.po
│       └── locale-fr_FR.po
├── services
│   ├── api
│   │   ├── scan.js
│   │   ├── storage.js
│   │   ├── subtitles.js
│   │   └── ...
│   ├── bus.js
│   ├── **events.js**
│   ├── **http.js**
│   ├── managers
│   │   ├── ScanManager.js
│   │   ├── ==UniverseManager.js==
│   │   ├── **volume.js**
│   │   └── ...
│   ├── Model.js
│   └── models
│       ├── channels
│       │   ├── TvChannel.js
│       │   └── ...
│       ├── dvb
│       │   ├── SatModel.js
│       │   └── SatTransponder.js
│       ├── index.js
│       ├── Subtitle.js
│       └── ...
├── utils
│   ├── CircularList.js
│   ├── **Controller.js**
│   ├── date.js
│   ├── Scrollable.js
│   ├── Singleton.js
│   └── ...
└── widgets
    ├── **Component.js**
    ├── index.js
    └── list




## Documentation du code
#### Génération de la doc
In project root :

```
$ npm run build-doc
```
La documentation sera accessible dans : [apps_frog-ui/esdoc/index.html](apps_frog-ui/esdoc/index.html) 

####Commentaires

- /!\ le tutoriel du HelloWorld n'est pas à jour, ne pas se fier au code proposé
- 10% des fonctions du code sont commentées

- *Classes*, *Fonctions* et *Variables* sont référencées ici : [apps_frog-ui/esdoc/identifiers.html](apps_frog-ui/esdoc/identifiers.html) 

- Les *webservices de l'API* sont regroupées en services et référencées ici : [apps_frog-ui/esdoc/source.html](apps_frog-ui/esdoc/source.html) 

	(ex : service volume.js inclut les webservices et/ou fonctions d'appels REST suivants : decreaseVolume, increaseVolume, getMute, mute, unmute)

- Les fonctions de tests unitaires : [apps_frog-ui/esdoc/test.html](apps_frog-ui/esdoc/test.html)


## HelloWorld 
(où mettre le nouveau code ? faire un schema avec les liens entre les fichiers modifiés- refaire une doc du HelloWorld)

####Create Component
create component (html)

	$ mkdir src/app/components/universes/HelloWorld
	$ touch src/app/components/universes/HelloWorld/index.js


style component

	$ touch src/app/components/universes/HelloWorld/index.css

add component to : src/app/components/index.js

- import component
 - add component to DOM tree

####Create Controller
create controller

	$ mkdir src/app/controllers/HelloWorld/
	$ touch src/app/controllers/HelloWorld/index.js

/!\ import new Controller to src/app/controllers/index.js >> doesn't exist

add "Hello World" item to Home Menu :
modify src/app/models/Home.js



## Retour d'expérience sur le code

- technologies en vogue, dernières nouveautés, en avance de phase (ES6 et css-next)
- code modulaire
- code maintenable (avec des conventions)
- dans le même esprit que les projets publiés sur github
- modèle MVC
- HelloWorld ==n'est pas à jour==, le code référencé a changé d'architecture et certains fichiers n'existent pas : retro-engineering nécessaire pour aller au bout de la spec du HelloWorld

>**Conclusion : **
>Le code est suffisamment générique, documenté et structuré, pour pouvoir s'y retrouver en se basant sur les exemples existants.
>Il a donc été possible de rajouter des composants simples utilisant les fonctionnalités existantes.




