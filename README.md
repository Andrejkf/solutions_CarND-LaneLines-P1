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


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

#### 1. Project Description. Describe your pipeline.

First off, on this project you will find the following folders:

* examples: Provided as part of project files.
* test_images: Provided as part of project files.
* test_videos: Provided as part of project files.

* step_by_step_images: In here you can follow up the step by step process on each test image.
* **test_images_output: final output images with detected lines.**

* test_videos_output _RGB_filter: output videos when apying RBG mask/filtering. **problem/opportunity in here:** On this one is easy to observe that predicted lines are very far away from the road in certain frames.

* test_videos_output-hough-transform: output videos with parameters on _hough transform_(threshold=1, min_line_len= 1, max_line_gap= 10)  before averaging lines (that is , before modifiying the provided _draw_lines()_ helper function. **problem/opportunity in here:** When averaging possible predicted lines (with function _draw_lines2()_ , that is my modification for the function _draw_lines()_ there is numerical inestability present on the returned values , co for the rest of the exercise I used as parameter for the _hough transform_(threshold=10, min_line_len= 10, max_line_gap= 5) 

* **test_videos_output: output videos as solution proposed for this project.** **problem/opportunity in here:** output averaged lines are very noisy/wavy/oscilatory during the road. basically I had noticed that **noise in lines** vary depending on the _color-space representation_, _noisy/non-smoothy borders after canny transform_ and  _parameters on hough-transformation_ mainly.










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
