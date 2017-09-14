# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "Solid Line on Right"
[image2]: ./test_images_output/solidYellowCurve.jpg "Solid Line on Left"

---


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I smoothed the image using a gaussian blur with a kernel size of 5. I then found the edges in the image using teh canny edge function. I cropped out the majority of the image using a mask function to only look at edges in the image that are likely to be the road. I used the hough function to find lines in that masked image. I then selected drew the left and right line on to the image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the gradient of all the lines I found using the hough function. I select only lines which are sloping towards the centre of the image. This is because this is the direction the lane lines predominantly follow. I further sort the images by gradient, if the gradient is negative then it means the line has been found on the left hand side of the image, if the gradient is positive then the line has been found on the right hand side of the image. I also look at the lengths of the sorted lines, this indicates which side of the car is a solid line and which side has a dashed line. If the line is dashed the car could entre this lane if needed so I colour those lines green however if it is a solid line then the car can't cross this line and so I colour it red. Ocassionally the pipeline fails and does not find suitable lane lines, in this situation the last successfully processed lane line positions are recalled. A recording is made of the number of times this occurs and so we can monitor the quality of the pipeline.

![image1]

![image2]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the the background of the road goes from light to dark in the challenge video it can confuse my method of determining which side of the road is free to enter. This could possibly be improved by normalising the greyscale distribution in the image. 

Another shortcoming could be traffic on the other side of the road when cornering. With the parameters as I have them set the can capture the cars. This could probably be overcome with more sophisticated masking.

