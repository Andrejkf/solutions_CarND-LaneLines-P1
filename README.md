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




---

## Reflection

### 1. Project Description.

##### 1.1. First off, on this project you will find the following folders:

* examples: Provided as part of project files.
* test_images: Provided as part of project files.
* test_videos: Provided as part of project files.

* step_by_step_images: In here you can follow up the step by step process on each test image.
* **test_images_output: final output images with detected lines.**

* test_videos_output _RGB_filter: output videos when apying RBG mask/filtering. **problem/opportunity in here:** On this one is easy to observe that predicted lines are very far away from the road in certain frames.

* test_videos_output-hough-transform: output videos with parameters on _hough transform_(threshold=1, min_line_len= 1, max_line_gap= 10)  before averaging lines (that is , before modifiying the provided _draw_lines()_ helper function. **problem/opportunity in here:** When averaging possible predicted lines (with function _draw_lines2()_ , that is my modification for the function _draw_lines()_ there is numerical inestability present on the returned values , co for the rest of the exercise I used as parameter for the _hough transform_(threshold=10, min_line_len= 10, max_line_gap= 5) 

* **test_videos_output: output videos as solution proposed for this project.** **problem/opportunity in here:** output averaged lines are very noisy/wavy/oscilatory during the road. basically I had noticed that **noise in lines** vary depending on the _color-space representation_, _noisy/non-smoothy borders after canny transform_ and  _parameters on hough-transformation_ mainly.


##### 1.2. Pipeline description

**Disclaimer!**: To make easier to follow up this reading I used just one image on this readme file, however, you can find all step_by_step process images on the folder **step_by_step_images**.

* Output images for this project can be found in folder **test_images_output** and output videos in folder **test_videos_output**. 

* There are two Ipython Notebook files. One before fine parameters tuning _p1-solution-without-parameter-tunning.ipynb_ and other one with fine parameter tuning included **p1-solution-parameter-tunning.ipynb**. you may want to check out the seccond one (**p1-solution-parameter-tunning.ipynb**).

My pipeline consist of 4 big steps ([Color Transformation](https://physics.info/color/),[Canny Edge detection](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjA-PXnnZ7YAhVBUd8KHcCSAIkQFggqMAA&url=http%3A%2F%2Fieeexplore.ieee.org%2Fdocument%2F4767851%2F&usg=AOvVaw0W14eP78FE6nl2CmMnqDtZ), [ROI ( Region Of Interest) selection](https://docs.opencv.org/3.3.0/d3/df2/tutorial_py_basic_ops.html), [Hough line Transform](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html)) that where splited out into **9 sub_steps:**

##### Color Transformation

###### 1.2.1 RGB color-space  vs HLS color-space

Images where loaded in RGB color-space. Inspired on [this document](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_colorspaces/py_colorspaces.html) I decided to check what happens if I apply _(Red,Green,Blue,Yellow_ and _White)_ __masks__ in **RGB color-space** and comparing them with _(Yellow,white)_ in **HSL color-space**.

First image is in _RGB- color space_ and Second image is in _HSL -color space_. It can be noticed that on seccond image ( _HSL -color space_ ) focused is more on the road than on sides parts of the road(or image sides). So **I used HLS- color transformation.**

* I used cv2.inRange() to filter yellow and white colors.
* I used cv2.bitwise_or to compute (yellow-mask) OR (white-mask)
* I used cv2.bitwise_and to apply previous mask to original image.

** Note:** this are values adjusted on trial/error.

For yellow color:
* Hue > 30
* Ligh = 0 = Not filtered
* Saturation > 90

For white color:
* Hue = 0 = not filtered
* Ligh > 180
* Saturation = 0 = Not filtered

![alt text][imagea]("solidYellowCurve.jpg in RGB-space") ![alt text][imageb]("solidYellowCurve.jpg in HLS-space")

###### 1.2.2 Grayscale representation

Before appying _canny algorithm_ images are mapped to _gray-scale_ representation. Images were transformed to gray-scale using cv2.cvtColor() function.

![alt text][imagec]("solidYellowCurve.jpg in gray scale")


###### 1.2.3 Grayscale representation
To avoid noise edge detection image is smoothed so that gradients (pixel intensity variations) can be detected easier. For that [cv2.GaussianBlur()](https://docs.opencv.org/3.0-beta/modules/imgproc/doc/filtering.html) was used. I used kernel size = filter size = 15.

![alt text][imaged]("solidYellowCurve.jpg in gaussian-blur")


##### Borders detection
Acording to documentation [cv2.Canny()](https://docs.opencv.org/3.1.0/da/d22/tutorial_py_canny.html), lower and upper threshold for border detection must be adjusted. However, is recommended in [here](https://docs.opencv.org/2.4/doc/tutorials/imgproc/imgtrans/canny_detector/canny_detector.html) to use a _upper:lower_ ratio between **2:1** and **3:1**.

Following values were selected:
* Upper threshold: 150
* Lower threshold: 50
* _upper:lower_ ratio : 150/50 = 3:1

###### 1.2.4.a. Edge detection
To detect borders cv2.Canny() function was used.

![alt text][imagee]("solidYellowCurve.jpg after canny edge detection")


###### 1.2.4.b. Morphological Transformations

After aplying canny edge detection. Noticed there are non continuous lines at the edge of _left-right_ road lines regions. So to reduce noise in the averaged _left-line region_ and _rigth-line region_, than is , to close up open regions [dilatation followed by erosion](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_morphological_ops/py_morphological_ops.html#dilation) was applied. For this, cv2.dilate() and cv2.erode() functions were used.

![alt text][imagef]("solidYellowCurve.jpg after dilation and erosion")


##### Region Of Interest (ROI) selection

###### 1.2.5.a. Generate image vertices

In order to reduce lines detection problem complexity, a focus region was introduced.

**Note:** At first attempt morphological transformation was not applied , so, averaged regions became noisy. To Improve that, my first insight was to  try different regions looking for noising out _spurious-contours_ close to the _left-rigth_ lines. I tried different region-shapes. But then I realized **most of power image noise ** is highly present in **non-closed** image regions. So I used the first polygon I initially tried out, a _truncated-triangle = trapezium_.

** Note2:** region vertices position calibration was done by _trial-error_. So, there should be an algorith to recalibrate those points while car is on the road, and the points here presented should be interpreted as _points-localization initialization_.

###### 1.2.5.b. Image mask-out

Region of interest selection was applied on preprocesed image by **blacking-out** positions _out of selected shape_. For this, cv2.fillPoly() function was used.

![alt text][imageg]("solidYellowCurve.jpg region to be focused")



##### Hough Transform

Once image is preprocessed and the region of interest is selected, **hough transform** is applied to find a set of posible detected lines that afterwards will be narrow down/average out.

###### 1.2.6 Compute Hough transform

In here v2.HoughLinesP() function was used.
**Note:** Hough transform parameters are very important in order to have good lines representation. In my case, Initially I had pseudo random parameter that gave me very noise predicted lines. But after tunning parameters, the best combinations I found was:

* (threshold=1, min_line_len= 1, max_line_gap= 10).

However, when afterwards when I averaged the predicted lines I had numerical inestability (so, **I need to improve my proposal to average out noise predicted lines**) and finally I used the following _hough transform_ parameter combination for the videos:

* (threshold=10, min_line_len= 10, max_line_gap= 5) 

With that setup predicted lines were still oscilatory/wavy/noisy.

![alt text][imageh]("solidYellowCurve.jpg Hough-lines transform")


So, the _set of possible lines_ on the road looks as follows:

![alt text][imagei]("solidYellowCurve.jpg with hough lines on the road")



##### connect/average/extrapolate output lines

This was the most challenging part for me because I had to modify the custom function **_draw_lines2()_** which is returning me back np.NaN values when I used this parameters set up in the hough transform: (threshold=1, min_line_len= 1, max_line_gap= 10). **This is an opportunity and space to improve my solution proposed.**

Here:

* Aproximated _left_ and _rigth_ linear functions are maped-back to the image space. 
* A helper function to return _averaged left-rigth lines_ as an array is defined.
* The provided helper function *weigthed_img* is used to aply trasnsparency to the predicted lines.
* Finally, predicted lines are painted over a copy of the original image.


###### 1.2.7 Get image pixels for averaged lines

On this subsection, output _predicted road lines_ are averaged out so than _a single representative line_ as output lane line is shown, one for the left side and one for the right side.

So, function **draw_lines** used in the hough transformation step was **modified and renamed as _draw_lines2()_** and can be seen 
in the IpythoNotebook with filename: _p1-solution-without-parameter-tunning.ipynb_

**Note:** on modified fuction **_draw_lines2()_** two variables are the important ones (**lineL, lineR**). The other variables where used to debug possible np.Nan returned values or empty list values.


![alt text][imagej]("solidYellowCurve.jpg with averaged predicted lines")


###### 1.2.8 Include the option to get _weighted predicted lines/trasparency in lines_

In this part, cv2.addWeighted() was used. with parameters:

* alpha=0.7
* betha=0.5
* color=[255, 0, 0] = Red
* thickness=10 = Predicted plotted line width.

###### 1.2.9. Predicted lines painted over original image

Custom function _lines_on_image()_  was defined to plot predicted trasparent lines over original test images. _lines_on_image()_ function can be seen in the IpythoNotebook with filename: _p1-solution-without-parameter-tunning.ipynb_. Below we can se how the final output looked like:

![alt text][imagek]("solidYellowCurve.jpg with averaged transparent lines")


---
### 2. Identify potential shortcomings with your current pipeline

* About **color space transformation**. HLS yellow-white mask _paraeters_ need further tuning to be less sensitive to higly variable  bright/light conditions.
* About **boders detection**. In the Canny algorithm parameters values also need to be adjusted to filter out spurious borders (undesired borders detection).
* About **region of interest (ROI) selection**. If the polygon base (trapecium base) is too wide or if the polygon heigh( trapecium heigh) is more than 0.6* Image_heigh, then many noise lines on the hough trasform are received and the slope for the predicted averaged line will change dramatically.
* About **Hough transform**. This is the part were the solution was returning np.Nan values whith parameters (threshold < 5 and min_line_len < 8 and max_line_gap < 15) whn using the modified _draw_lines2()_ function to get the _averaged predicted line_. And more specifically in the values for the predicted rigth line or when testing on the video challenge.mp4. And this phenomena happens for high changes in bright/light images and small changes when computiong the gradients on edge detection. For that reason, further image processing or data processing need to be done to make the output predicted lines somoother.


### 3. Suggest possible improvements to your pipeline

* A possible improvement on the **color space transformation** subsection would be to try out better ways to be more robust to abrup changes in bright on images.
* Another unexplored task is on the **boders detection** subsection, when using the functions cv2.dilate() and  cv2.erode(), to try out different kernel sizes and number of iterations in the cross correlation _between the filter and the image_.
* Also, a potentional improvement would be on the **region of interest (ROI) selection** subsection, to try out different polygons regions. Also AI algorithm to tune the vertices localization in the images would be better when implementing code on real scenario, for example Q-learning.

* Another potential improvement is on the way to average out the noise predicted lines so that smother predited lines can be provided.


---
[//]: # (Image References)

[imagea]: ./step_by_step_images/a_rgb-mask/5.png "solidYellowCurve.jpg in RGB-space"

[imageb]: ./step_by_step_images/b_hls-mask/5.png "solidYellowCurve.jpg in HLS-space"

[imagec]: ./step_by_step_images/c_gray-scale/5.png "solidYellowCurve.jpg in gray scale"

[imaged]: ./step_by_step_images/d_gaussian-blur/5.png "solidYellowCurve.jpg in gaussian-blur"

[imagee]: ./step_by_step_images/e_canny/5.png "solidYellowCurve.jpg after canny edge detection"

[imagef]: ./step_by_step_images/f_dilate-erode/5.png "solidYellowCurve.jpg after dilation and erosion"

[imageg]: ./step_by_step_images/g_region-mask/5.png "solidYellowCurve.jpg region to be focused"

[imageh]: ./step_by_step_images/h_hough-transform/5.png "solidYellowCurve.jpg Hough-lines transform"

[imagei]: ./step_by_step_images/i_lines-on-road/5.png "solidYellowCurve.jpg with hough lines on the road"

[imagej]: ./step_by_step_images/j_aproximated-lines-on-road/5.png "solidYellowCurve.jpg with averaged predicted lines"

[imagek]: ./step_by_step_images/k_aproximated-lines-on-road-transparency/5.png "solidYellowCurve.jpg with averaged transparent lines"





