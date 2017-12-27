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

![alt text][imagea]("solidYellowCurve.jpg in gray scale")

###### 1.2.3 Grayscale representation
To avoid noise edge detection image is smoothed so that gradients (pixel intensity variations) can be detected easier. For that [cv2.GaussianBlur()](https://docs.opencv.org/3.0-beta/modules/imgproc/doc/filtering.html) was used. I used kernel size = filter size = 15.

[imaged]: ./step_by_step_images/d_gaussian-blur/5.png "solidYellowCurve.jpg in gaussian-blur"

##### Borders detection
Acording to documentation [cv2.Canny()](https://docs.opencv.org/3.1.0/da/d22/tutorial_py_canny.html), lower and upper threshold for border detection must be adjusted. However, is recommended in [here](https://docs.opencv.org/2.4/doc/tutorials/imgproc/imgtrans/canny_detector/canny_detector.html) to use a _upper:lower_ ratio between **2:1** and **3:1**.

Following values were selected:
* Upper threshold: 150
* Lower threshold: 50
* _upper:lower_ ratio : 150/50 = 3:1

###### 1.2.4.a. Edge detection
To detect borders cv2.Canny() function was used.
[imagee]: ./step_by_step_images/e_canny/5.png "solidYellowCurve.jpg after canny edge detection"

###### 1.2.4.b. Morphological Transformations

After aplying canny edge detection. Noticed there are non continuous lines at the edge of _left-right_ road lines regions. So to reduce noise in the averaged _left-line region_ and _rigth-line region_, than is , to close up open regions [dilatation followed by erosion](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_morphological_ops/py_morphological_ops.html#dilation) was applied. For this, cv2.dilate() and cv2.erode() functions were used.

[imagef]: ./step_by_step_images/f_dilate-erode/5.png "solidYellowCurve.jpg after dilation and erosion"

##### Region Of Interest (ROI) selection

###### 1.2.5.a. Generate image vertices

In order to reduce lines detection problem complexity, a focus region was introduced.

**Note:** At first attempt morphological transformation was not applied , so, averaged regions became noisy. To Improve that, my first insight was to  try different regions looking for noising out _spurious-contours_ close to the _left-rigth_ lines. I tried different region-shapes. But then I realized **most of power image noise ** is highly present in **non-closed** image regions. So I used the first polygon I initially tried out, a _truncated-triangle = trapezium_.

** Note2:** region vertices position calibration was done by _trial-error_. So, there should be an algorith to recalibrate those points while car is on the road, and the points here presented should be interpreted as _points-localization initialization_.










---
[//]: # (Image References)

[imagea]: ./step_by_step_images/a_rgb-mask/5.png "solidYellowCurve.jpg in RGB-space"

[imageb]: ./step_by_step_images/b_hls-mask/5.png "solidYellowCurve.jpg in HLS-space"

[imagec]: ./step_by_step_images/c_gray-scale/5.png "ssolidYellowCurve.jpg in gray scale"

[imaged]: ./step_by_step_images/d_gaussian-blur/5.png "solidYellowCurve.jpg in gaussian-blur"

[imagee]: ./step_by_step_images/e_canny/5.png "solidYellowCurve.jpg after canny edge detection"

[imagef]: ./step_by_step_images/f_dilate-erode/5.png "solidYellowCurve.jpg after dilation and erosion"

[imageg]: ./step_by_step_images/g_region-mask/5.png "solidYellowCurve.jpg region to be focused"

[imageh]: ./step_by_step_images/h_hough-transform/5.png "solidYellowCurve.jpg Hough-lines transform"

[imagei]: ./step_by_step_images/i_lines-on-road/5.png "solidYellowCurve.jpg with hough lines on the road"

[imagej]: ./step_by_step_images/j_aproximated-lines-on-road/5.png "solidYellowCurve.jpg with averaged predicted lines"

[imagek]: ./step_by_step_images/k_aproximated-lines-on-road-transparency/5.png "solidYellowCurve.jpg with averaged transparent lines"





