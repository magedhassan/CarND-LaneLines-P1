# **Finding Lane Lines on the Road**
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

The goal of this project is to detect lane lines in images and videos using Python and OpenCV. The result shall be creating an output image or video where two solid lines are drawn to highlight the driver's lane.

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining the solution.

The code file is called P1.ipynb and is located at the same path as this README.md file.

This file (README.md) is the writeup that explains the solution.


Contents
---
This file will include the following sections:

1. Description of the pipeline

2. Identification of shortcomings

3. Possible improvements


1. Description of the pipeline
---
The pipeline works on an image or on a video which is no more than a series of images.

The tools we are going to be using are color selection, region of interest selection, grayscaling, Gaussian smoothing, Canny Edge Detection and Hough Tranform line detection.

#### The original image
One test image looks as follows:

![image](/test_images/solidYellowCurve2.jpg)

#### The grayscale image
First we convert the image to a grayscale one to avoid working on a color space that will make the process more complicated.

![gray](/Images for README/gray.jpg)

#### The smoothed grayscale image
Then we apply Gaussian smoothing to blur the contrast in the image to avoid having too many edges when we apply Canny algorithm.

![smoothed gray](/Images for README/blur_gray.jpg)

#### The edges image
Then using Canny algorithm we detect the edges in the image.

![smoothed gray](/Images for README/edges.jpg)

#### The masked_edges image
We choose only the edges in our region of interest which is a polygon in the driver's view. This will isolate the edges related to the lane lines.

![masked edges](/Images for README/masked_edges.jpg)

#### The line_image image
We can then identify lines using Hough Transform and highlight them using solid colored lines.  

![line_image](/Images for README/line_image.jpg)

#### The final image
We then add the line image to the original image to show the lane lines on the original image.

Doing the previous steps on each video frame will result in a new video but with the lane lines marked in real time.

![lines_edges](/Images for README/result.jpg)

2. Identification of any shortcomings
---
This method needs a lot of manual adjustments of parameters which can result in the pipeline working well with some images on which the parameters have been adjusted, but on the other hand could not work so well with other images where the lane line characteristics are different in shape or color or continuity.   

Possible source of errors:
- The manual adjustments of parameters for Hough Transform could greatly affect detecting the correct lane lines.

- Averaging the lane lines could result in a lines outside the actual lane line.

- Lane lines with curvature will not be efficiently detected by this pipeline.


3. Possible improvements
---
- Better determintation of the driver view will help identifing the correct region of interest, which shall in turn help discarding any false detected lines in the view.

- I believe using some machine learning techniques will help without the sole dependency on lane lines detection using image analysis.
