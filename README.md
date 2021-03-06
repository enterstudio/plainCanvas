#plainCanvas

Adobe Illustrator (CC 2014-2018) add-on with following functions.  
(Japanese README is [here](https://github.com/shspage/plainCanvas/blob/master/README_ja.md))

* loads and executes a script file written for [paper.js].  
(at the initial state, you can use a simple drawing tool.)
* exports the image created on the panel onto the artboard.
* imports selected paths on the artboard onto the panel.
[paper.js]:http://paperjs.org

![image of the panel](https://github.com/shspage/plainCanvas/raw/master/image/desc_plaincanvas.png "image of the panel")

###Installation
Because of the character of this add-on that loads external script files, it is released with an assumtion of doing debugs.  Installation steps are as follows.  

1. Setting the __debug mode flag__ refer to Adobe's document [CC14_Extension_SDK.pdf] at page 10.  
2. Put the folder "com.shspage.csxs.plaincanvas" in the right folder refer to the page 5 of above document ("Extension management" section).  
3. Launch Illustrator and navigate Window -&#62; Extensions fo find plainCanvas.

[CC14_Extension_SDK.pdf]:http://wwwimages.adobe.com/content/dam/Adobe/en/devnet/creativesuite/pdfs/CC14_Extension_SDK.pdf

###buttons on the panel
* __in__ : imports selected paths on the artboard onto the panel
* __out__ : exports the image created on the panel onto the artboard
* __opt__ : shows/hides the form for optional values
* __&#60;__ : undo
* __&#62;__ : redo
* __CL__ : clears the panel
* __DB__ : opens the debug tool with a default browser.
* __RL__ : reloads the panel
* __select__ : selects a script file to load

###script files that can be loaded
* There're some sample scripts in "[scripts](https://github.com/shspage/plainCanvas/tree/master/scripts)" folder.  
* Write in __JavaScript__ (not paperscript).  For details, see "[Using JavaScript Directly]" in http://paperjs.org.  
__ex:__ new Path() -> new paper.Path()  
__ex:__ point1 + point2 -> point1.add(point2)  
__ex:__ function onMouseDown(event) -> tool.onMouseDown = function(event)  
* Set the character encoding to __UTF-8__.
* You can use the UIs for optional values with simple methods. see "js/optionManager.js".
* You can set a drawn object as a target for undo/redo by calling the method like this.
```javascript
undoManager.keep(object);
```
Note that undoed objects are just hidden, and still exists in the current paper.project.
[Using JavaScript Directly]:http://paperjs.org/tutorials/getting-started/using-javascript-directly/



###colors
* Since html5 canvas uses RGB color, imported CMYK and GRAY colors may look different from they look on the artboard.
* If ALWAYS_EXPORT_RGB (js/main.js) is set false, the original CMYK colors are kept in memory
and are applied when they are exported. (When DefaultColorSpace of the artboard
is CMYK.)
* If ALWAYS_EXPORT_RGB is true, GRAY colors are exported in RGB.
* Gradient color and spot color are not supported for now.

###exports to an artboard
* Following attributes of paper.Path instance on the canvas are exported.  
_segments, strokeWidth, strokeColor, fillColor, opacity_

###imports from an artboard
* Following attributes of selected PathItems are imported.  
_pathPoints, strokeWidth, strokeColor, fillColor._
* Grouped paths and compoundpaths are imported in released condition.

###License
* When you distribute a modified version, make sure changing the __bundle ID__.
It is represented as "com.shspage.csxs.plaincanvas" in CSXS/manifest.xml and .debug.
*  Copyright (c) 2015 Hiroyuki Sato. All rights reserved.  
http://shspage.com/  
This software is distributed under the MIT License.  
See the LICENSE.txt for details.  
This software uses the following libraries that may have
licenses differing from that of the software itself. You can find the
libraries and their respective licenses below.

* Paper.js v0.9.23 - The Swiss Army Knife of Vector Graphics Scripting.  
http://paperjs.org/  
Copyright (c) 2011 - 2014, Juerg Lehni & Jonathan Puckey  
http://scratchdisk.com/ & http://jonathanpuckey.com/  
All rights reserved.  

* Creative Cloud Extension Builder for Brackets  
https://github.com/davidderaedt/CC-Extension-Builder-for-Brackets  
Copyright (c) 2012 Adobe Systems Incorporated. All rights reserved.  

