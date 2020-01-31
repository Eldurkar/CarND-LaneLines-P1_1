# **Finding Lane Lines on the Road** 

## Writeup

**The goals / steps of this project**
* Make a pipeline that finds lane lines on the road
* Reflect on the steps and possible improvement in a written report
---

## Reflection

### 1.  Set up:
About a day was taken up in completing the system set up necessary for the project.  This included the installation, set up and learning of Anaconda, Git/Github and Jupyter Notebook.  Then using pip to get the necessary python modules for this project. Not sure this counts as a performance marker, but it was fun and without it the project could not be started.

---
### 2.  Pipeline description: 

The code file is called P1_1.ipynb

**Modification of the draw_lines() function:**
The draw_lines() function was modified to use the detected line segments and combine them to form the left and right lanes.
The pipeline has the following steps -
1.  Create lists to store the right and left slopes and centers for each of the line segments.
2.  Iterate over the line segments to calculate the slopes and centers.
3.  The calculated slopes and centers were then appended to the right or left lists, while rejecting slopes that were to steep or too flat.
4.  The slopes were used to get an average slope for the left lane and an average slope for te right lane.
5.  As with the slopes, the centers were used to find a single center for the right lane and left lane.
6.  The y coordinate of the left and right line(lane marking) was set to roughly 60% of the image height.
7.  The slope, center and y coordinate were plugged in to the line equation to ultimately get the four coordinates required to create the lines.

**Modification of the draw_lines() and hough_lines() functions for the optional challenge:**
The draw_lines() function was renamed to draw_linesChallenge() to keep the changes above separate from the one above. Though not as good as I would have liked, the curvature of the road was followed. The lanes were created after sorting the centers of the line segments going from the bottom of the image to the top.  The centers of the lines were then used to create new line segments. Here are the steps in the pipeline: 
1.  The draw_linesChallenge() has the same initial steps 1 through 3, as the draw_lines() function above.
2.  The list of line centers was sorted in order to be able to loop though the points an create a line.
3.  The sorted list of coordinates was then used to draw line segments for the right and left lanes.

To use the draw_linesChallenge() function, the hough_lines() function was modified to call this function.  The hough_lines() function has a line that reads #draw_linesChallenge(line_img, lines). Toggle (comment /uncomment) between this line and the #draw_lines(line_img, lines) line to execute the optional challenge.

---
### 3. Identify potential shortcomings with your current pipeline

1.  Shades of concrete/markings:  Find a way to deal with lighter shades of road when the white lane markings blend in with the color of the road. This was observed on a small section of the optional challenge video. Stray dark lines on a light colored road can also trick the canny edge detection function.
2.  Road barrier:  A road barrier which runs right next to the lane that has a light colored appearance would get included within the region of interest with lane lines being drawn on it. This was also seen in the optional challenge.
3.  Lighting:  While driving at night or in poor light conditions it can be difficult to identify the lane markings.
4.  Curved roads:  Roads with a small radius of curvature would need a different algorithm to create a continuous and smooth lane marking.


### 3. Suggest possible improvements to your pipeline

1.  Using tangents to define a curved lane and then creating the lane markings using the tangential points to create a curved lane.
2.  Writing optimization functions for canny edge and hough lines parameters to improve on the captured line markings.

In general, it might be possible to improve finding lanes using machine learning techniques such as neural networks.