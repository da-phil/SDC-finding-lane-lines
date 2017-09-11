# Finding Lane Lines on the Road

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/whiteCarLaneSwitch.jpg "Example image"

---

### Reflection

### 1. Pipeline description

**Edge detection**

I applied the canny edge detector on the gray image. This works quite well independend of colours, as long as there is enough contrast. The usual settings of 100 / 200 for the low and high tresholds delivered good results.

**Reign of interest selection**

Masking out a triangle area which stretches from far left to right and a height of 0.45 of the image height was sufficient. I started out with a symmetrical trapazoid, but it was not so well suited, it left too much clutter on the top left and right.

**Finding lines**

The hough transformation was used on masked edges to extract lines. I chose the parameters so that there is a good tradeoff between filtering out lines and keeping enough lines in the result for the lane line estimation. The resolution in the parameter spaces was chosen to be 1px for `rho` and 1° for `theta`. The `hough_threshold` was set to 20, `min_line_len` to 80px and `max_line_gap` to 50px.

**Filtering and extrapolation**

I'm filtering the lines by their slope. If the lines are within the slope thresholds the get assigned into left lane and right lane groups, otherwise they are considered as outliers. After collection all x and y datapoints for the left and right lane it used a least squares fitting to obtain a good estimate for the slope and intercept for final lane lines.


Here is a result from the given example images, the green lines highlight the detected lines and the red ones show the final left and right lane lines:
![alt text][image1]


### 2. Potential shortcomings with the pipeline

* Not using additional colour information on lanes, which could be helpful in tricky cases
* Lanes are only estimated as lines, polynomials or splines would be more accurate
* Parameters of pipeline are not generic and need to be adjusted for each car, camera, camera mounting position, lighting conditions etc.


### 3. Possible improvements to the pipeline

* Use colour segmentation
* Implement polynomial or spline fitting for lanes
* Use online parameter estimation or machine learning techniques to tune parameters according current situation
