#### solutions_CarND-LaneLines-P1

# **Finding Lane Lines on the Road** 

This is the project one for term one. The main goal is to be able to **detect/draw road lines** in a set of test provided incoming images and videos(sequential set of images).

I used [anaconda](https://www.anaconda.com/) Python flavour (version 3.6.1) and an open source library python dedicated for image and deep learning called [OpenCV](https://opencv.org/releases.html) (version 3.1.0).

For my solution proposed, the next techniques were applied:
* [Color Transformation](https://physics.info/color/).
* [Canny Edge detection](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjA-PXnnZ7YAhVBUd8KHcCSAIkQFggqMAA&url=http%3A%2F%2Fieeexplore.ieee.org%2Fdocument%2F4767851%2F&usg=AOvVaw0W14eP78FE6nl2CmMnqDtZ).
* [ROI ( Region Of Interest) selection](https://docs.opencv.org/3.3.0/d3/df2/tutorial_py_basic_ops.html)
* [Hough line Transform](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html)

This is a non exclusive list of openCV functions I used:
* [cv2.cvtColor()](https://docs.opencv.org/3.2.0/df/d9d/tutorial_py_colorspaces.html) , [cv2.inRange()](https://docs.opencv.org/3.2.0/df/d9d/tutorial_py_colorspaces.html), [cv2.bitwise_or()](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_colorspaces/py_colorspaces.html) , [cv2.bitwise_and()](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_colorspaces/py_colorspaces.html). Used for color space transforms.
* [cv2.Canny()](https://docs.opencv.org/3.1.0/da/d22/tutorial_py_canny.html). Used for gradients computation(edge/borders detection).
* [cv2.GaussianBlur()](https://docs.opencv.org/3.0-beta/modules/imgproc/doc/filtering.html). Used for image filtering(2d cross correlation).
* [cv2.line()](https://docs.opencv.org/3.1.0/dc/da5/tutorial_py_drawing_functions.html). Used to draw lines.
* [cv2.HoughLinesP()](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html). Used for Hough-image space transform.
* [cv2.addWeighted()](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_core/py_image_arithmetics/py_image_arithmetics.html). Used for image blending.


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
