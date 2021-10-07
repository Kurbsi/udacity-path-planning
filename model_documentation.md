## Write Up

### Detect objects around

The algorithm for path plannig starts at line 100. To know possible trajetories for the ego vehicle, we need to know which lanes are potential candidates for driving. To evaluate this we need to get an understanding of objects in our vicinity. 

This is calculated from line 110 on. We check the the different lanes and keep a flag per lane indicating if this lane is occupied or not. For our current lane we only check the area of 30 m in front of us (line 121-125). For the lanes next to us we check the area from 30 m behind up to 30 m in front of us (line 126-138).

If we detect that a car is in our lane and that the car in front of us is slower than our car, we reduce our velocity every step by 0.23. In addition we check if a lane next to us available. If a lane is available we increase or decrease the *lane* variable depending on which lane is available.

If no car is in front of us, we also check if our current vel (ref_vel) is below the max velocity of 50, we increase the reference velocity by 0.224 (line 152).

### Generate path

To generate a proper path we first add points which are either based on the previous calculated path or, if there is now previous path, we calculate based on the current position and heading of the car (line 170 - 195). 

Next we extrapolate the three points with a distance of 30 m, 60 m and 90 m (line 196-198). Given these five points we calculate a spline and divide the spline into 50 points each with the same distance apart (line 218ff). 