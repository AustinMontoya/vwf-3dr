# ADL 3DR Integration with Virtual World Framework

This code is a proof of concept highlighting the ability to use the ADL's [3D-Repository](https://github.com/adlnet/3D-Repository) to integrate with the [Virtual World Framework](https://github.com/virtual-world-framework/vwf) currently being developed by Lockheed Martin for the US Department of Defense. It provides the ability for users to search publicly downloadable models from the main 3D Repository, drag them into a VWF instance, and add them to the scene. It also provides VERY BASIC translation and scale manipulation (someone please fork and implement rotation!). 

## Platforms

This has currently only been tested with the latest stable release of Chrome.

## Installation 

1. Have a working instance of the Virtual World Framework downloaded and installed.
1. Download or clone this repo.
1. Copy the contents of the public folder into `<vwf_root>/public/`
1. Copy `3drmodel.vwf.yaml` into `<vwf_root>/support/proxy/vwf.example.com/`
1. We need to patch `C:\dev\vwf\support\client\lib\vwf\model\glge\glge-compiled.js` to support cross-origin texture requests. In `GLGE.Texture.prototype.setSrc`, add the following line immediately after line 6868:
```javascript
this.image=new Image(); 
this.image.crossOrigin = "anonymous"; // this is the new line to add
```
1. Start the vwf server. Open two browser windows and point them both to http://localhost:3000/3dr. Use the sidebar on the left to search the 3DR (hint: try `nasa` or `case`). Drag the image of the model you want to add to the scene onto the scene. It will load after a few seconds. You can then click on the model for a small menu that allows you to manipulate the basic properties of the object.