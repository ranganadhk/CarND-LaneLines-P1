# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

1) Grayscale image 2) Gaussian blurring(noise cancellation) 3) Canny edges transform to identify edges 4) Application of masking to get only region of interest or eliminate edges outside the region of interest 5) Application of Hough transform to get Hough Lines from above and extrapolation of lines by seperating lines in right and left lane (by sign of slope) and drawing single line bewteen extremities (see draw_lines function) 6) Another application of mask to get only region of interest or eliminate edges outside the region of interest 7) Finally, Combine resulting lanes image with original image using weighted_img to get final result.

### 2. Identify potential shortcomings with your current pipeline

I see that the pipeline failing with intersecting and incorrect lane markings while processing the "challenge.mp4". Main challenge  seems to be due to: 1) shadows, spurious lines, and other markings on the road that are wrongly classified as "lines" and extrapolated 2) Another challenge would be extreme curvature of the roads. 3) some broken white lines are drawn stright solid lines in some frames that can be rectified.

### 3. Suggest possible improvements to your pipeline

Improve the draw_lines function that extrapolates the hough lines to draw the lanes. 1) To address shadows, spurious markings: This can be done by eliminating those hough lines, whose slope are outliers (not belonging within the general range of other slopes within the right and left lines respectively). This can be done by removing quartiles using IQR to remove 10-15% on both sides. At a minimum removing lines with the most extreme slopes in right and left lines would also help 2) Extreme road/ lane curvature: Using higher order polyfit routine over the x,y coordinates for the right and left lanes respectively. I will do this if I get time and re-submit.
