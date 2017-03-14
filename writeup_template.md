##Writeup Template
###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Vehicle Detection Project**

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector. 
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)
[image1]: ./output_images/hog.png
[image2]: ./output_images/boxes1.png
[image3]: ./output_images/boxes2.png
[image4]: ./output_images/boxes3.png
[image5]: ./output_images/heatmap.png
[image6]: ./output_images/finalboxed.png
[image7]: ./output_images/
[video1]: ./labeledcarsfull_video.mp4

## [Rubric](https://review.udacity.com/#!/rubrics/513/view) Points
###Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Vehicle-Detection/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

###Histogram of Oriented Gradients (HOG)

####1. Explain how (and identify where in your code) you extracted HOG features from the training images.

The code is in the python notebook CarND-Vehicle-Detection.ipynb in function get_hog_features. Function used from udacity example.

####2. Explain how you settled on your final choice of HOG parameters.

I took default parameter from udacity example and it worked.

####3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

I used hog, spatial and histogram features. And used these to train LinearSVC classifier. The code is in CarND-Vehicle-Detection.ipynb, where linearSVC is used.

###Sliding Window Search

####1. Describe how (and identify where in your code) you implemented a sliding window search.  How did you decide what scales to search and how much to overlap windows?

The code is in CarND-Vehicle-Detection.ipynb, in function find_cars. The scale and overlap was determined by experimenting on where the cars might be in the image wrt to horizon and their relative size.

In label_cars function there are lists that define different regions to search in.

####2. Show some examples of test images to demonstrate how your pipeline is working.  What did you do to optimize the performance of your classifier?

Didn't try optimizing performance, just used udacities hog subsampling as it is.

Hog:
![alt text][image1]

Different box sizes:
![alt text][image2]
![alt text][image3]
![alt text][image4]

Heatmap:
![alt text][image5]

Final boxed:
![alt text][image6]

---

### Video Implementation

####1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives.)
Here's a [link to my video result](./project_video.mp4)


####2. Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.

For filtering false positives I used heatmap and thresholding it. And then the min-max boundary of this heatmap as the bounding box.  

---

###Discussion

####1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Issues faced:
- Effective and more coverage results in longer computation time
- Frame to frame changing size of bounding boxes - not so smooth feel

Pipeline will fail if:
- with lot of cars on the road, that is overlaping images of cars
- likel fail in low light or night scenes

