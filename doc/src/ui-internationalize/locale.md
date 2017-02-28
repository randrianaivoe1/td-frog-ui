

### Questions

### Installation
[Portal doc](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/framework/locale/) 

##### Prerequisites for locale.sh script to run

babel to extract translatable content from js files

	$ sudo apt-get install babel

python-babel python module for Babel

	$ sudo apt-get install python-babel

gettext to use msginit tool to create (*.po) translation files

	$ sudo apt-get install gettext

[locale-po to json](https://pypi.python.org/pypi/pojson) 

	$ sudo apt-get install python-pip
	$ sudo pip install pojson

##### Poedit : GNU for translators
[Online doc](https://poedit.net/) 

	$ sudo apt-get install poedit


### How to

1. Changer la langue de l'interface :
via le menu
traduction à la volée des menus de configuration
/!\ atttention si changement de la langue via le code - ce n'est pas géré (faut passer par le menu)
>
requête PUT config/settings/locale
update de la Home

2. Ajouter une nouvelle langue à traduire
>
Modifier la variable LOCALES dans locale.sh
Lancer le script pour générer le .po
Lancer le script pour mettre à jour index.js

3. Rajouter des chaînes de caractères traductible


### Workflow
![](/home/randrianaivoe1/Documents/i18n.png) 

### Script générateur "locale.sh"
- configure available languages
- create POT from JS source files in [apps_frog-ui/src] (cf. 1)
	
	/!\ add output args "-o" to define output file
	
- merge with POT added manually (cf. 1)
- create PO (cf. 1) :
run script for each new language (cf. 2)
previous existing PO files will be moved in a ~file.po
- create final JS file used by i18n module (cf. 4)


### Référencement des chaînes à traduire : état actuel du code
> 
- pas unifié
- Il faut identifier les chaînes qui sont à traduire, elles peuvent être encapsulées dans différentes structure de données ou variables (e.g : items.label, attributes.comment.default)
- Les chaînes répertoriées manuellement dans manual/*.pot ne précisent pas le référencement au fichier source

### Implémentation de l'internationalisation dans le code
**locales/index.js** 
> LOCALE_DATA

**utils/locale.js**
>
*class i18n*
- charge les LOCALE_DATA et fournit la traduction d'une chaîne dans la langue
	/!\ autant d'instance que de langue
	
>
*class Locale*
	- instantie un i18n à partir des LOCALE_DATA et la langue demandée
	- fournit les fonctions de traduction d'une chaîne de caractère ou d'un ensemble d'élément du DOM
	- envoie un evenement lors d'un changement de langue via le menu

**app/utils/locale.js **
> translate DOM (SettingsMenu, manualRecord and ScanProgress-services-found) already loaded
envoie un event après traduction "locale:update"


**_("translate me")**
services/manager
app/utils/PopUpMsg.js
app/models
app/controllers
app/components

**listeners to "locale:update"**
app/controllers/Home > rechargement du menu
app/controllers/PVR > 
app/controllers/Settings > 

### Commentaires
Un joyeux bazar (pas unifié - même script à lancer plusieurs fois et qui va faire des actions différentes à chaque fois)


Découper le script : 
src_to_pot, pot_to_po (merge and add new languages), po_to_js

Référencer au moins les noms de fichier dans les POT manuel et préfixer TOUTES les chaînes à traduire par _("")
