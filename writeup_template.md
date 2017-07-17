# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./gray.png "Grayscale"

[image2]: ./blurred.png "Blurred"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps :

1. First I converted the image to grayscale image. As it is easier to do image processing techniques on a grayscale image. The image is displayed below

![Grayscale][image1]

2. I then used the Gaussian Blur function to remove noise in the grayscale image. This smoothens the variation in intensity throughout the image. The blurred image is displayed below
![Blurred][image2]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
