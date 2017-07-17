# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./images/gray.png "Grayscale"

[image2]: ./images/blurred.png "Blurred"

[image3]: ./images/edged.png "Edged"

[image4]: ./images/masked_image.png "Masked Image"

[image5]: ./images/lines_image.png "Line Image"

[image6]: ./images/final_line_image.png "Final Line Image"

[image7]: ./images/output.png "Output Image"

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps :

1. First I converted the image to grayscale image. As it is easier to do image processing techniques on a grayscale image. The image is displayed below

![Grayscale][image1]

2. I then used the Gaussian Blur function to remove noise in the grayscale image. This smoothens the variation in intensity throughout 
the image. The blurred image is displayed below

![Blurred][image2]

3. I then used the in built Canny function to identify the edges in the image.  This involved experimenting with two parameters namely a 

lower threshold and a higher threshold to determine which pixels are truly edges. Finally I was able to obtain an image of the edges 

(which is a binary image with edged pixels = 255 and non-edge pixels = 0) as shown below :

![Edged][image3]

4. The next step was to define a region of interest by identifying the vertices of a quadrilateral which best encompassed the two lanes.
Using the following vertices : {[150, image.shape[0]],[455, 315],[510 , 315],[900, image.shape[0]]}, I was able to get the following
image:

![Masked Image][image4]

5. Now we have the our masked image which contains only the edges of the lanes. I then applied HoughTransformP function to identify 
which pixels are lines and obtain their x and y positions. Using these I drew all the lines on the image to obtain the line_image as 
shown below:

![line image][image5]

6. Modifying the draw_lines function:

In order to extrapolate the line segments and draw them on the image, I carried out the following steps:

a. Initially I looped through each set of points identified by the Hough Transform.

b. I then found the slope  for each of the lines and picked out the slopes above a certain magnitude.

c. Then based on the sign of the slope and x co-ordinate I was able to group the x and y co-ordinates of the points based on whether 
they belong in the left lane or right lane.

d. Then using all the points in the left lane, I used the polyfit function to fit a straight line through the points. And repeated the 
process for the right lane.

e. I then started to identify the extreme points of each lane. For the bottom extreme points, I knew the y co-ordinates (simple the 
height of the image), and using my parametrized lane I obtained the corresponding x co-ordinates for each of those points.

f. The top extreme points were trickier. The initial solution I used was simply the maximum of the left x co-ordinates for the left 
lane. And the minimum of the right x co-ordinates for the right lane. While this did a reasonably good job for the left lane. The minimum x co-ordinates in the right lane had too much variance. So I took an average of all the min x co-ordinates of the right lane for all images and used this instead.

g. The corresponding y co-ordinates for each of the x co-ordinates were evaluated by using np.poly1d(np.polyfit) function.

h. Finally the lines were drawn on the line image using the cv2.line function.

The image is shown below:
![Final Line Image][image6]

7. The last step was combining the line_img and original image using the weighted_add function. I used an alpha of 0.7, beta of 0.3 and lmabda of 30.

![Output Image][image7]


### 2. Identify potential shortcomings with your current pipeline

1. One potential shortcoming is that my pipeline may not be robust to variation in illumination of the images.

2. Another shortcoming is identifying the top extreme points. Currently I will not have access to all the minimum right x co-ordinates, so technically I cannot use this information.

3. A final shortcoming might be the fact that I fit a straight line through the co-ordinates of each of the lanes. If the lane was not really straight, then drawing a straight line on the image may not capture the lanes.

### 3. Suggest possible improvements to your pipeline

1. A possible improvement would be to fit a higher order polynomial through the points. Thus allowing us to draw over curved lanes as well.

2. 
