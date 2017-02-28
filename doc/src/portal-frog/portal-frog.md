# GENERAL ARCHITECTURE

[General architecture](https://portal.frogbywyplay.com/docs/wytv/featured/arch_diagram/) 
![](/home/randrianaivoe1/Pictures/A-full-archi.png) 

**SOFTWARE LAYER COMMUNICATION**
![](/home/randrianaivoe1/Pictures/architecture-com.png) 

- Wyrest uses a notification mechanism defined  [here](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/wyrest/http/routes/#get--events-) to notify events to applications via  [SSE](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) (Server-Sent Event) 

- HTTP routes provided by Wyrest are listed [here](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/wyrest/http/routes/) 

- List of methods implemented by middleware components and exposes through DBus API : [interfaces](https://portal.frogbywyplay.com/docs/wytv/featured/toc-interfaces/) 

## A. FROG-UI
[OVERVIEW](https://portal.frogbywyplay.com/docs/wytv/featured/components/apps-frog-ui/overview/) 
![](/home/randrianaivoe1/Pictures/C-frog-ui.png) 


## B. WYREST
wyrest is a RESTful API, it exposes all the middleware functionalities through HTTP and communicates with middleware component through the D-Bus API.

[Code, Présentation, Fonctionnalités, Howto, Références ](https://portal.frogbywyplay.com/docs/wytv/featured/components/appframeworks-wyrest/overview/) 

![](/home/randrianaivoe1/Pictures/E-wyrest.png) 


## C. MIDDLEWARE
### 1. MW-PVR
[All components](https://portal.frogbywyplay.com/docs/wytv/featured/components/toc-media/) 

![](/home/randrianaivoe1/Pictures/F-PVR.png) 


##### SRS
[SRS](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-srs/overview/)  :  Scheduled Recording Service, respecte la norme UPnP SRS. Expose API over D-Bus not over network

Flexible architecture to support evolutions > ==TO BE VERIFIED==
	![](/home/randrianaivoe1/Pictures/L-SRS.png) 

[cds-tv](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-cds-tv/overview/#cds-tv) : EPG provider component : process DVB Service information tables and provides list of channels

[strategy](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-strategy/overview/#strategy) : resolve conflicts btw recordings

##### MEDIARENDERER2
[MEDIARENDERER2](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-mediarenderer2/overview/) : default record launcher (audio/video streams) : play, record, pause, stop, rw, ff, select A/V and subtitle

![](/home/randrianaivoe1/Pictures/M-mediarenderer.png) 

[config-store](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-config-store/overview/#config-store) : manage configuration through DBus or C++ API (content parameters, parental control, protection)


##### WYPLAYER
[WYPLAYER](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-wyplayer/overview/): multimedia player responsible for rendering audio and video. ==See compatibility with supported stantards.==


##### WYCAS
[WYCAS](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-libwycas/overview/) : built-in features to CAS integrators 
- filter PMT sections to descramble live DVD services 
- filter CAT sections to receive EMM sections

	/!\  limitations : i/ currently only work with unique CAS Driver ii/ no D-Bus interface for operator specific objects like purchases

### 2. MW-SYSTEM-MANAGEMENT

![](/home/randrianaivoe1/Pictures/G-system-management.png) 

##### wystorage
[wystorage](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wystorage/overview/) : mount disks/USB keys
##### platformd-wyclock
[platformd-wyclock](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-platformd-wyclock/overview/) : time system
##### network manager
[network manager](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wynetwork/overview/) : network interface configuration, monitoring connections/disconnections, list available networks
##### wystandby
[wystandby](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-wystandby/overview/) : manages the power state of the board (ready, standby, suspend, low-pwer, wake-up alarm)


### 3. MW-CONTENT-HANDLING

![](/home/randrianaivoe1/Pictures/H-contenthandling.png) 

##### cds-pvr
[cds-pvr](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-cds-pvr/overview/) : monitors the local list of recordings, which is populated by other components

![](/home/randrianaivoe1/Pictures/Q-cds-pvr.png) 

##### downloader
[frogbywyplay.com](https://frogbywyplay.com/) 


##### wyscan
[wyscan](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-wyscan/overview/)

		-  framework enabling scan DVB transponders and retrieve the Service Information tables
		-  hosts cds-tv : services list ( includes fav. lists) and EPG
	/!\ you have to implement a plugin with yout product-specific scanning algorithm
![](/home/randrianaivoe1/Pictures/P-wyscan.png) 


### 4. MW-PLATFORM-ADAPTATION
![](/home/randrianaivoe1/Pictures/J-platform-adaptation.png) 

##### avio
[avio](https://portal.frogbywyplay.com/docs/wytv/featured/devkit/components/porting-platformd-nexus-avio/overview/) : dead link

##### wyrender
[wyrender](https://portal.frogbywyplay.com/docs/wytv/featured/components/media-wyrender/overview/) : interface to be implemented in order to display frames : it allows hardware-specific graphical display operations

##### wydvb 
[wydvb](https://portal.frogbywyplay.com/docs/wytv/featured/components/contents-wydvb/overview/) : manages DVB tuners of the Set-top box


### 5. MW-OTHER
![](/home/randrianaivoe1/Pictures/K-other.png) 

##### config-store
[config-store](https://portal.frogbywyplay.com/docs/wytv/featured/components/system-config-store/overview/) : manages configuration for all components - through DBus or C++ APIs

##### wylog
[wylog](https://portal.frogbywyplay.com/docs/wytv/featured/components/utils-wylog/overview/) : library to manage component logs. Itis configurable.

##### 
[wytransport](https://portal.frogbywyplay.com/docs/wytv/featured/components/utils-libwytransport/overview/) : gives access to multimedia content WITH PUGINS FOR TRANSPORT PROTOCOLS LIKE http, https, http/dlna, smb
