# Finding Lane Lines on the Road

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Pipeline description

* Applying canny edge detector on gray image. Works quite well independend of colours. Chose the following parameters:
* Masking out a symmetrical trapazoid area with the following parameters: ...
* Finding lines by applying hough transformation on masked edges. Chose the following parameters:
* Filtering lines by their slope and assigning lines into left lane and right lane groups. Used least squares fitting to fit final lane lines.

![alt text][image1]


### 2. Potential shortcomings with the pipeline

* Not using additional colour information on lanes, which could be helpful in tricky cases
* Lanes are only estimated as lines, polynomials or splines would be more accurate
* Parameters of pipeline are not generic and need to be adjusted for each car, camera, camera mounting position, lighting conditions etc.


### 3. Possible improvements to the pipeline

* Use colour segmentation
* Implement polynomial or spline fitting for lanes
* Use online parameter estimation or machine learning techniques to tune parameters according current situation
