**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell of the IPython notebook located in "./project.ipynb".

I have defined the find_chessboard_corners function reads the chess board images and detects the inner conners of chess board.
This result is used to find the distrotion matrix for further process.

Each image converted to grayscale before passing to opencv provided `findChessboardCorners()` funtion. 

The detected coners of the example images is shown below: 

![result][/output/camera_calibrated.png]


#### 2. Distortion-correction on images.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2]

From the result obtained from `findChessboardCorners()` function (objpoints, imgpoints) I called c`alibrateCamera()` funtion of opencv obtain the distrotion matrix 

The values returned by `cv2.calibrateCamera()` will be used later to undistort our video images.

The sample results on a chess board image and test image is shown below:

![alt text][output/undistroted_img.png]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The cperspective transform is called using a function called `birds_eye()`, in the 5th cell of the IPython notebook.  The `birds_eye()` function takes as inputs an image (`img`) along with few argument s to display and read images.  I chose the hardcode the source and destination points in the following manner:

```python
    src = np.float32([[490, 482],[810, 482],
                      [1250, 720],[40, 720]])
    dst = np.float32([[0, 0], [1280, 0], 
                     [1250, 720],[40, 720]])
```
The result applied perspective tranform is shown below:

![alt text][output/wraped_image.png]


#### 4 Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image. 

Here's is the result obtained from each and combination of both:

![alt text][output/thershold.png]

#### 5. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

#### 6. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

#### 7. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

All these three steps i did in a single funtion named `fill_lane()` which comes in the 17 cell of my code.

The function takes an image as input it findes the lane pixels.

Then it calculate the radius of curvature of both the left and right lanes detected (left_curverad,right_curverad).

Once the lanes are detected on the wrapped image I tried to plot it back to the orginal image resulting the following output

![alt text][output/lane_fitting_in_orginal_img.png]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_result.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

I tried different methods to get a better thershold and found the combination looks much better.
But i am doubted the result on a show road, where the lanes are not much clear
