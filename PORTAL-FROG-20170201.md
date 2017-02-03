#Documentation du code
Accessible via : [apps_frog-ui/esdoc/index.html](apps_frog-ui/esdoc/index.html) 


- NB: 10% des fonctions du code sont commentées

- Toutes les *classes*, les *fonctions* et les *variables* sont référencées : [apps_frog-ui/esdoc/identifiers.html](apps_frog-ui/esdoc/identifiers.html) 

- Tous les* webservices de l'API* sont regroupées en services et référencées ici : [apps_frog-ui/esdoc/source.html](apps_frog-ui/esdoc/source.html) 

	(ex : service volume.js inclut les webservices et/ou fonctions d'appels REST suivants : decreaseVolume, increaseVolume, getMute, mute, unmute)

- (??) tests [apps_frog-ui/esdoc/test.html](apps_frog-ui/esdoc/test.html)

#Documentation Portail  - Frog Client

[GENERAL ARCHITECTURE](https://portal.frogbywyplay.com/docs/wytv/featured/arch_diagram/) 
![](/home/randrianaivoe1/Pictures/A-full-archi.png) 


### A. FROG-UI
[OVERVIEW](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/overview/) 
![](/home/randrianaivoe1/Pictures/C-frog-ui.png) 


### B. WYREST
L'API WYREST expose les fonctionnalités du Middleware via HTTP. Il communique avec le middleware par le D-Bus.
[Code, Présentation, Fonctionnalités, Howto, Références ](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/overview/) 
[sytème de notification via les SSE](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/wyrest/http/routes/#get--events-) : remonte les évènements aux applications.

![](/home/randrianaivoe1/Pictures/E-wyrest.png) 


### C. MIDDLEWARE
#### 1. MW-PVR
[all components](https://portal.frogbywyplay.com/docs/wytv/featured/components/toc-media/) 

![](/home/randrianaivoe1/Pictures/F-PVR.png) 


1.  [SRS](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-srs/overview/)  : Scheduled Recording Service, respecte la norme UPnP SRS. Expose API over D-Bus not over network

	Flexible architecture to support evolutions > ==TO BE VERIFIED==
	![](/home/randrianaivoe1/Pictures/L-SRS.png) 

	[cds-tv](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-cds-tv/overview/#cds-tv) : EPG provider component

	[strategy](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-strategy/overview/#strategy) : resolve conflicts btw recordings

2.  [MEDIARENDERER2](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-mediarenderer2/overview/) : default record launcher (audio/video streams) : play, record, pause, stop, rw, ff, select A/V and subtitle

	![](/home/randrianaivoe1/Pictures/M-mediarenderer.png) 

	[config-store](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-config-store/overview/#config-store) : manage configuration through DBus or C++ API (content parameters, parental control, protection)


3.  [WYPLAYER](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-wyplayer/overview/): multimedia player responsible for rendering audio and video. ==See compatibility with supported stantards.==


4.  [WYCAS](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-libwycas/overview/)

		built-in features to CAS integrators a) filter PMT sections to descramble live DVD services b) filter CAT sections to receive EMM sections
		/!\  limitations : i/ currently only work with unique CAS Driver ii/ no D-Bus interface for operator specific objects like purchases

#### 2. MW-SYSTEM-MANAGEMENT

![](/home/randrianaivoe1/Pictures/G-system-management.png) 

[wystorage](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wystorage/overview/) : mount disks/USB keys
[platformd-wyclock](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-platformd-wyclock/overview/)  : time system
[network manager](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wynetwork/overview/) : network interface configuration, monitoring connections/disconnections, list available networks
[wystandby](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wystandby/overview/) : namages the power state of the board (ready, standby, suspend, low-pwer, wake-up alarm)


#### 3. MW-CONTENT-HANDLING

![](/home/randrianaivoe1/Pictures/H-contenthandling.png) 

[a. cds-pvr](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-cds-pvr/overview/) : monitors the local list of recordings, which is populated by other components

![](/home/randrianaivoe1/Pictures/Q-cds-pvr.png) 

[b. downloader](https://frogbywyplay.com/) : frogbywyplay.com
[c. wyscan](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-wyscan/overview/) : 

		-  framework enabling scan DVB transponders and retrieve the Service Information tables
		-  hosts cds-tv : services list ( includes fav. lists) and EPG
	/!\ you have to implement a plugin with yout product-specific scanning algorithm
![](/home/randrianaivoe1/Pictures/P-wyscan.png) 

[cds-tv](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-cds-tv/overview/#cds-tv)  : process DVB Service information tables and provides list of channels & EPG


#### 4. MW-PLATFORM-ADAPTATION
![](/home/randrianaivoe1/Pictures/J-platform-adaptation.png) 

[avio](https://portal.frogbywyplay.com/docs/wytv/featured/devkit/components/porting-platformd-nexus-avio/overview/) : dead link
[wyrender](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-wyrender/overview/) : interface to be implemented in order to display frames : it allows hardware-specific graphical display operations 
[wydvb](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-wydvb/overview/) : manages DVB tuners of the Set-top box


#### 5. MW-OTHER
![](/home/randrianaivoe1/Pictures/K-other.png) 

[config-store](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-config-store/overview/) : manages configuration for all components - through DBus or C++ APIs

[wylog](https://portal.frogbywyplay.com/docs/wytv/featured/components/utils-wylog/overview/) : library to manage component logs. Itis configurable.

[wytransport](https://portal.frogbywyplay.com/docs/wytv/featured/components/utils-libwytransport/overview/) : gives access to multimedia content WITH PUGINS FOR TRANSPORT PROTOCOLS LIKE http, https, http/dlna, smb
