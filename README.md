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

Images were transformed to gray-scale using cv2.cvtColor() function.
![alt text][imagec]("solidYellowCurve.jpg in gray scale representation")




---
[//]: # (Image References)

[imagea]: ./step_by_step_images/a_rgb-mask/5.png "solidYellowCurve.jpg in RGB-space"
[imageb]: ./step_by_step_images/b_hls-mask/5.png "solidYellowCurve.jpg in HLS-space"

[imagec]: ./step_by_step_images/c_gray-scale/5.png "solidYellowCurve.jpg in HLS-space"
[imaged]: ./step_by_step_images/d_gaussian-blur/5.png "solidYellowCurve.jpg in HLS-space"
[imagee]: ./step_by_step_images/e_canny/5.png "solidYellowCurve.jpg in HLS-space"
[imagef]: ./step_by_step_images/f_dilate-erode/5.png "solidYellowCurve.jpg in HLS-space"
[imageg]: ./step_by_step_images/g_region-mask/5.png "solidYellowCurve.jpg in HLS-space"
[imageh]: ./step_by_step_images/h_hough-transform/5.png "solidYellowCurve.jpg in HLS-space"
[imagei]: ./step_by_step_images/i_lines-on-road/5.png "solidYellowCurve.jpg in HLS-space"
[imagej]: ./step_by_step_images/j_aproximated-lines-on-road/5.png "solidYellowCurve.jpg in HLS-space"
[imagek]: ./step_by_step_images/k_aproximated-lines-on-road-transparency/5.png "solidYellowCurve.jpg in HLS-space"




