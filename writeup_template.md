# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

My pipeline consisted the following steps
1. Yellow and white filters applied through the HSV color map
2. Conversion of the filtered image to grayscale
3. (Only for videos) Frame averaging of the grayscale image. An IIR filter with coefficient 0.5 was used. 
   * This helps in the challenge video when the lane lines are obscured in shadows. Filtering enables detection even under those circumstances.
3. Gaussian blur applied on the grayscale image
5. Canny edge detection 
6. Region masking to isolate the edges within the expected region in the camera image
7. Hough transform to identify the lines from the edges within the regions
8. Modified the draw_lines function to draw the left and the right lanes. 
   * To do this, I first identified the edges whose slopes where consistent with expected ones for the left and right lanes respectively. Once they were identified and classified into two sets, I fit a straight line through all the points in the two sets respectively. I then used this fit to draw lines from the bottom of the image to the top of the region mask.

### 2. Identify potential shortcomings with your current pipeline

One limitation was that curves in the lanes could result in misalignments with the lines that I drew. 

Another limitation resulting from fitting a line through the points (rather than connecting the individual hough lines) was that the fitted line would be sensitive to an outlier. This results in a very slight jitter of the drawn lines in the movie.


### 3. Suggest possible improvements to your pipeline

Possible improvements are
1. Curve fitting to the points in the hough line set instead of line fitting
1. Use the average slope to classify the lines into left and right sets. Instead of drawing a line through each set, connect the end points of each segment and extrapolate to region boundaries
