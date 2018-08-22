# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
---
My pipeline consisted of the following steps :
- Conversion to grayscale image .
- Gaussian smoothing .
- Canny edge detection .
- Region of interest selection .
- Line segments detection using Hough transform .
- Drawing lane lines on a blank image .
- Blending the two images to produce the final image . 
  
---
### In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following steps :
- Filtering Detected line segments and classifying them into right lane line segments and left lane line  segments based on the slope .
- Averaging the endpoints of the detected right and left lane line segments .
- Fitting a straight line model to the end points of the averaged right and left lane line segment. 
- Extrapolating the right and left lane lines to the top and bottom boundaries of the region of interset to form solid lane lines .
- Drawing the final lane lines
 --- 
### **Observations** :
 
- This pipeline worked well with images and videos having straight lane lines . 
- **Shortcoming** : In videos , lane lines were jumping / flickering due to the change of their positions from one frame to another .
- **Modification** : In order to stabilize and smooth the lane lines , I modified ```draw_lines()``` function to ```draw_lines_improved()``` functions which deployed a moving average approach by Keeping tracking of the slopes and intercepts of the right and left lines detected and fitted in each frame and storing them in a buffer then averaging those parameters over the last N frames and using them to perform extrapolation and draw the lane lines and filling the pixels inside the lane with green color .  

---
### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are curved/bent lane lines .

---

### 3. Suggest possible improvements to your pipeline

- A possible improvement would be to deploy weighted moving average which applies higher weights to the most recent frames

- Another potential improvement could be using higher-order polynomial rather than the straight line to better fit the curved lane lines . 

- In addition , more improvement can be done by using deep learning to predict  polynomial coefficients which would give better and more accurate results .

### Note :

- I applied the previous pipeline to the challenge video and it gave quite good results with a modification at the begining of the pipeline by adding  color selection step which takes advantage of HSL color space in order to isolate the white and yellow lane lines in different lighting conditions and blackout the car hood and other objects such as trees and other cars on the road .

- In my quest , I managed to fit a 2nd order polynomial to the end points of the detected right and left line segments but I searched many times and wasn't able to find a way to draw such polynomial curves given start point , end point and polynomial coefficient a,b,c  in opencv .  
