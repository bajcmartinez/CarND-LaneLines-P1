# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[pipeline1]: ./examples/pipeline1.png "Pipeline - Step 1"
[pipeline2]: ./examples/pipeline2.png "Pipeline - Step 2"
[pipeline3]: ./examples/pipeline3.png "Pipeline - Step 3"
[pipeline4]: ./examples/pipeline4.png "Pipeline - Step 4"
[pipeline5]: ./examples/pipeline5.png "Pipeline - Step 5"
[pipeline6]: ./examples/pipeline6.gif "Pipeline - Step 6"

---

## Pipeline


### 1. Capture the screen essence

In this first step we try to capture the relevant aspects of the picture. For that we apply color selection to the image, we processes all the white and yellow colors and then we convert it to grayscale. This strips most of the things away leaving us with the lanes and some noise to work on.

![alt text][pipeline1]

### 2. Smoothing of the lines

We apply Gaussian Blur to smooth out the picture.

![alt text][pipeline2]

### 3. Edge detection

We use canny algorithm for edge detection.

![alt text][pipeline3]

### 4. Crop the region of interest

To remove noise from the picture (e.g. sky, trees, etc that we could not remove before) we crop the picture assuming that the camera is in the center of the car on a fixed position.

![alt text][pipeline4]

### 5. Hough Transformation

Next we apply hough transformation to detect the lines in the picture.

![alt_text][pipeline5]

### 6. Final step to draw 2 lines that mark the full lane

In here we use a linear regression to join all the lines provided by Hough's algorithm.

![alt_text][pipeline6]

## Potential issues

1. It is not hard to recognize that the code would only work while on rects or very smooth curves
2. There is also an issue that would happen when the car is transitioning lanes
3. Any factor that may alter the colors on the picture can play a major role in the identification (weather, very dirty lanes, etc)
4. Polyfit algorithm used for the linear regression is very sensitive to outliers, this is causing major issues. Even if I applied an outliers filter based of an statistical model it is still not 100% accurate and some circunstances trigger the lines to severly deviate from the standard.

## Future work
1. Use ML for better identification of the relevant aspects of the picture and also for outliers detection
2. Make it work on curves and transitioning lanes
3. I believe this model is not highly scalable and that a whole new approach needs to be introduce to make it work on more real applications.
