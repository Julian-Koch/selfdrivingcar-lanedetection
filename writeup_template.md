# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/output_solidWhiteRight.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps in total.
1) I converted the images to grayscale.
2) I applied Gaussian Blur on the grayscale image
3) I used Canny edge detection on that image
4) I defined a region of interest by defining 4 vertices of a rectangle to limit the picture
5) I used the Hough transformation in order to find lines in the picture
6) I used the modified draw lines function (in detail below) to draw solid lines on the picture
7) I combined to original image with the hough lines so the lines could be seen on the actual picture

In order to draw a single line I altered the drawlines() function.
To identify values of the left and right line I used positive and negative slope values.
I collected m (slope) and b (interception) values in an array and defined a mean function to calculate the average value for left and right line. Then I used these to define the right and left line with the bottom of the picture as starting point and the end of the mask as the end value.

In the end I used a for loop to iterate over all pictures and save them to a output directory.

Then I tuned the parameters until the results over all pictures where statisfying.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Example picture of the result][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be when the car drives on bad or damaged pavement, the camera will shake and the algorithm will have difficulties to get clean values. In the current code there is no filter to retain peaks.

Another shortcoming is that lines in different distances result in different qualities of lines painted over them. If a line on the street is missing it could result in the algorithm to fail.

Another shortcoming is that the data that the algorithm is trained with is really limited and also that testing is done manually. A bigger training set in combination with a parameter tuning algorithm and a algorithm to evaluate the results could improve the quality of the lane detection.

The video results are not 100% statisfying since the lines appear to be "jitter". This could be improved by using mean values of more than more pictures instead of calculating a new line for every picture.

### 3. Suggest possible improvements to your pipeline

Improvements are mentioned in 2 after the several shortcoming.
