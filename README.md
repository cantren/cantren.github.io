# cantren.github.io

SimBox - Robosub is a derived work which incorporates code from multiple authors.

Original Author(s):

@author WestLangley / http://stackoverflow.com/users/1461008/westlangley/

@author Jos Dirksen / http://www.github.com/josdirksen/learning-threejs/

#Copyright Notices:
"SimBox" is derived from "github.com/josdirksen/learning-threejs/", Copyright 2015 Jos Dirksen
github.com/josdirksen/learning-threejs/ is distributed under the terms of the GitHub Terms of Service

"SimBox" incorporates code from "github.com/josdirksen/learning-threejs/", Copyright 2015 Jos Dirksen
github.com/josdirksen/learning-threejs/ is distributed under the terms of the GitHub Terms of Service
 
"SimBox" is derived from "http://stackoverflow.com/a/16227714", Copyright 2014 WestLangley
Stack Exchange Subscriber Content is distributed under the terms of the Stack Exchange Terms of Service
http://stackexchange.com/legal/terms-of-service

"SimBox" incorporates code from "http://jsfiddle.net/aqnL1mx9/", Copyright 2014 WestLangley
http://jsfiddle.net/aqnL1mx9/ is distributed under the terms of the jsFiddle.net Terms of Service
http://doc.jsfiddle.net/meta/credits.html#license

The MIT License

Copyright © 2010-2015 three.js authors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

#Copyright Notes:
* Code primarily reflects the authors of the three.js examples under the MIT License 
"http://threejs.org/examples/webgl_shaders_ocean.html"
and
"http://threejs.org/examples/webgl_loader_obj_mtl.html"

* Please Note:
The most heavily borrowed code(that isn't from three.js examples) is actually from the work of an unnamed jsFiddle.net author(previously unattributed user, possibly identified as "WestLangley") who is assumed to be the same stackoverflow user who answered a question about a downward facing camera here: http://stackoverflow.com/a/16227714

#Housecleaning
* Almost none of josdirksen's code remains: consider forking the repository, then rolling that fork back to a previous commit such that it accurately reflects the attribution, then sanitizing the remainder of borrowed code. Credit to josdirksen will then be preserved in the README.md.
* UPDATE: more josdirksen code has been added(sort of) at cantren.github.io/Install Instructions/server setup.txt http://www.smartjava.org/content/capture-canvas-and-webgl-output-video-using-websockets






# What is SimBox?

“SimBox” is a cross-platform simulation environment developed by Nicholas Cantrell that runs in any WebGL capable web 
browser(such as Chrome.exe). It was developed in order to allow new students to rapidly gain a high level of proficiency with 
autonomous vehicle software development without the high barriers to entry created by making a mechanically and electrically 
integrated robot submarine a prerequisite to testing software.

# Live Demo:
http://cantren.github.io

#How it works:
The control scheme should be familiar to anyone that has played PC-based First-Person-Shooter genre games, with the slight 
modification that vertical mouse position controls Submarine depth instead of camera “pitch”.


ASDW controls should be intuitive to many new students. The horizontal mouse cursor position on the screen controls “yaw”, 
and the keyboard input are used to control the vehicles translation through the water.


The bottom left hand corner shows a “bottom facing camera” which is used to identify and orient the submarine relative to the 
orange “path markers” which are placed along the competition mission path every year by the organizers of the AUVSI Robosub 
Competition.


The bottom right hand corner shows a “preview window” square white box. This is used to preview the computer vision filter 
perspective while the software is running. For more information, please see “Integration/Interface”.


# Integration/Interface:
The API for “SimBox” is based on Human Interface Device input, as well as an FFMPEG video software program called “ffserver” 
which allows for the client(computer connected to cantren.github.io) to run a local server on their PC for the SimBox 
“Preview Window” to display.


The video that is broadcast from this local server(http://127.0.0.1:8090/simbox.swf) ultimately must be generated on-the-fly 
using screen capture software(FFMPEG + X11Grab)[Linux] OR (FFMPEG + Screen Capture Recorder)[Windows] which is used to record 
a live screencast to ffserver feed #1. 

OpenCV’s “VideoCapture” class uses this “feed #1” as its input stream, does the necessary processing on it, and then outputs 
the post-filtering feed to the ffserver “feed #2”(IE. http://127.0.0.1:8090/simbox.swf).


When in “autopilot mode”, the OpenCV server will take control of the mouse and keyboard. A demonstration of this can be found 
at the following url:

https://github.com/cantren/Vunit[Linux Version]

[TODO: make Windows version][Windows Version]

# Feature Request(s)
At this time, a universal interface using a Teensy 3.0 to emulate HID input has not been considered a priority use of limited 
resources, however people interested in developing this functionality are encouraged to do so.

# Further Reading:
https://trac.ffmpeg.org/wiki/Capture/Desktop [CLI syntax overview]
https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu [X11Grab]
http://sourceforge.net/projects/screencapturer/files/ [Screen Capture Recorder]

# FFMPEG Setup
[TODO: write FFMPEG installation/quickstart guide for Windows & Linux]
