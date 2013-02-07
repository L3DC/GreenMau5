GreenMau5
=========

Author: Ethan Green (Partner of L3DC)
  
This program is an adaptation of the work started by Noah Huppert.

This program has been tested on OSX 10.8.2 and Windows 7. It must be put into a directory containing the LeapJava.jar to work.

The way in which the x and y locations are found on the screen has
been changed as well as the way clicking works. Scrolling was removed
for the time being.

Variable settings:

Time: The system time taken for each step of animation. Increasing this may lead to smoother mouse movement, but it may also lead to lag. Time should be 0 or greater.

Smoothing: The number of steps taken when the mouse is moved to a new step. Increasing this can lead to better 
looking mouse movement; however, if the smoothing is too high it will result in slow movement. Smoothing should be 1 or greater.

Count: The number of iterations through the while loop on which the next frame will be recieved. Increasing this can lead
to a stedier mouse, but it may also result in mouse lag. Count should be 2 or greater.

If you find any particular settings that work well, please let us know.
