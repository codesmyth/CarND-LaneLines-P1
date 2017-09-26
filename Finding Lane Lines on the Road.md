# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./writeup_images/edges.png "Edges"
[image3]: ./writeup_images/region.png "Region of Interest"
[image4]: ./writeup_images/hough.png "Hough Transformation"
[image5]: ./writeup_images/final.png "Final image with weighted lines"
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The lane finding pipeline has been defined as a function consisting of 6 steps. First, I converted the images to grayscale[image1], then I applied Gausian blur to the grayscale image. I then used canny edge detection to identify edges[image2]. I defined a function to create the list of vertices for a region mask and applied this to effectively narrow the field of vision[image3]. Hough lines[image4] then weighted image is calulated and overlayed onto the original image[image5].

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
using the gradients of the line segments from the hough lines transformation to separate the points appearing on the left lane from those appearing on the right lane. I created a collection of right line points and left line points. I noticed that some outliers in these points lists casued the line to miss the lane, so I removed any points that sat 1.5 standard deviations from the mean of the x (horizontal) coordinate. I used the numpy polyfit function to get the slope and intercept of straightline for both the right and left lane points. I identified the apex of the left and right lines by looking for the right most and left-most points respectivley and extended the base of each line to the base of the image. I then used cv2.line to produce the lines on the original image.    

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be when other lines with a positive or negative gradient exist inside the region of interest and close enought to the fitted line such that they aren't treated as outliers,these outliers would direct the line away from the line it's meant to follow.

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to one a lane line is identified use it's attributes, gradient to further remove outliers with the same sign(+/-) that are not parallel 

Another potential improvement could be to ...
