Stereoscopic Rendering in Blender 2.6
=================
Addon version 1.6.8, by Sebastian Schneider.

Manual copied from (http://www.noeol.de/s3d/)

Introduction
============
How to implement an off-axis camera to produce correct stereo pairs via Python Add-on in Blender

Since there is no stereoscopic camera in Blender, I decided to write a python script to implement an 'Off-Axis' stereo camera. This script sets the 'Stereo Window' or zero parallax in Blender and not via postproduction. It creates a parallel off-axis camera rig, the best way to produce stereo pairs without [vertical parallax](http://www.noeol.de/s3d/vertical_parallax.html). You can use Blenders Node Editor to control the left and right camera render results and combine them to a Side-by-Side, Interlaced or Anaglyph image.

![](http://www.noeol.de/s3d/gui.png)
![](http://www.noeol.de/s3d/frustum.png)

Videos
======
* [Video tutorial](http://www.youtube.com/watch?v=HFhKxocDqnA) (youtube.com)
* [How to render a stereo Side-by-Side animation](http://www.youtube.com/watch?v=usWXat4pt1M) (youtube.com)

Camera Types
============

The Add-on provides all three stereoscopic camera types. The 'Off-Axis' rig is set as default, because of its best results. The 'Converge' (or Toe-In) Camera rig is only useful if you have to match 'real-stereo-camera' material due to its tendency to produce [vertical parallax](http://www.noeol.de/s3d/vertical_parallax.html). The 'Parallel' Camera produces always negative parallax, which means that all objects appearing later in front of the screen and you have to set the zero parallax manually. Recommendation: If you want to do some good and easy to fuse stereo pairs, use the default Off-Axis Camera rig only.

![](http://www.noeol.de/s3d/offaxis_rig.png) 
![](http://www.noeol.de/s3d/toein_rig.png) 
![](http://www.noeol.de/s3d/parallel_rig.png)

Note: to re-calculate the shift of the Off-Axis Camera, click the 'Set Stereo Camera' button
 1. if you change the render resolution
 2. if you change the camera angle
 3. if you change any stereo parameter

(if the output is a Side-by-Side: delete the nodes and click 'Add-Nodes' again to get the new size too)

Mathematics
===========

For those who are interested in off-axis calculation and how to build the [stereo comfort zone](http://www.noeol.de/s3d/near-far-plane.png)], here are some formulas.

1) Calculating off-axis shift (delta) in pixel:

![](http://www.noeol.de/s3d/delta_form.png)

b = stereo base (horiz. separation of left and right camera)
w = render width in pixel
f0 = focal distance to zero parallax (stereo window)
FoV = horiz. Field of View (camera angle)

2) Calculating [max. disparity](http://www.noeol.de/s3d/sleep.png) (disp) in pixel at near- and far-plane (simple sine rule):

![](http://www.noeol.de/s3d/disp_form.png)

theta = max. parallax angle, given by the user (default 1.0°)
vdist = distance between viewer and projection screen
ppi = Pixel Per Inch of the projection screen

3) Calculating distance (pdist) to near- and far-plane to get the [stereo comfort zone](http://www.noeol.de/s3d/near-far-plane.png):

![](http://www.noeol.de/s3d/pdist_form.png)

b = stereo base (horiz. separation of left and right camera)
delta = off-axis shift of the first formular in pixel
disp = max. disparity at near- and far-plane (2nd formular) in pixel (disp is for Nearplane '+' and for Farplane '-')
FoV = horiz. Field of View (camera angle)

4) Calculating the 'Toe-In' angle in degree for the converge camera rig:

![](http://www.noeol.de/s3d/toein_form.png)

b = stereo base (horiz. separation of left and right camera)
f0 = focal distance to zero parallax (stereo window)
