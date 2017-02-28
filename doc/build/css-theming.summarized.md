# <a name =0></a> Table of content
  + [How to custom Frog-ui Styling](#1)
      + [Main theme colors](#2)
      + [Height, width](#3)
      + [Menu](#4)
      + [Background (midnight) in Popup Vod and Notification](#5)
      + [Vod font color (cyan)](#6)
      + [Splashscreen and app background (dark midnight)](#7)
      + [Clock font color (clear blue) and clock background](#8)
      + [Vod spinner](#9)
  + [Conclusion](#10)
## <a name ="1"></a> How to custom Frog-ui Styling ([&#8632;](#0))
#### <a name ="2"></a> Main theme colors ([&#8632;](#0))
Change color values in :
> app/components/globals.css

#### <a name ="3"></a> Height, width ([&#8632;](#0)) 
Values in :
> app/components/globals.css

#### <a name ="4"></a> Menu ([&#8632;](#0))
- **selector**
*Image to be replaced for custom* :
> app/assets/buttons/vertical-selected-gradient.png
	
- **icons**

*Add*, replace or delete *icons* in : 
> app/assets/anims

References in :
>app/components/universes/Home/index.css

#### <a name ="5"></a> Background (midnight) in Popup Vod and Notification ([&#8632;](#0))
Currently hardcoded, need to be replaced by global variale --unFocused
> app/components/universes/Application/PopUp/index.css
> app/components/universes/Application/PopUp/index.css
> app/components/universes/Vod/index.css
> app/components/widgets/Notification/index.css

#### <a name ="6"></a> Vod font color (cyan) ([&#8632;](#0))
Currently hardcoded, need to be replaced by global variable  --Dominant
> app/components/universes/Vod/index.css


#### <a name ="7"></a> Splashscreen and app background (dark midnight) ([&#8632;](#0))
Currently hardcoded, a global variable should be created
> app/components/universes/Apps/index.css
> app/components/universes/SplashScreen/index.css

#### <a name ="8"></a> Clock font color (clear blue) and clock background ([&#8632;](#0))
Font color in :
> app/components/universes/Application/Clock/index.css

*Image might be replaced* here :
> app/assets/backgrounds/clock.png

#### <a name ="9"></a> Vod spinner ([&#8632;](#0))
*Replace following image with custom* :
> app/assets/pictos/vod-bubble.png

## <a name ="10"></a> Conclusion ([&#8632;](#0))
1. A little refactoring is needed to ease changes and future evolution :

	- any reusable colors should be allocated to a global variable in globals.css - with a short description
	- all image url should not be hardcoded but assigned to variables indexed in a file or on top of each file

1. Front-end developpers or CSS integrators can easily modify and improve this code.
1. Icons and image replacement requires graphic designer skills and associated software (e.g : photoshop)
