Track an Object in 3D Space
===========================

## FP.0 Final Report

*Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf.*

This is my report for the project.

## FP.1 Match 3D Objects

*Implement the method "matchBoundingBoxes", which takes as input both the previous and the current data frames and provides as output the ids of the matched regions of interest (i.e. the boxID property). Matches must be the ones with the highest number of keypoint correspondences.*

I used a OpenCV `Mat` to store the counts of all the keypoint matches mapping each bounding box pair. To compute these counts I have iterated over all the matches to find all the bounding boxes the two keypoints are contained in and incremented the corresponding matrix value. I then scanned each row of the matrix to find the bounding boxes in the current frame with the maximum amount of keyframes for each bounding box of the previous frame.

## FP.2 Compute Lidar-based TTC

*Compute the time-to-collision in second for all matched 3D objects using only Lidar measurements from the matched bounding boxes between current and previous frame.*

When viewed from the top-view, the lidar points of the car looks very much aligned, so there is not much difference in the x-coordinate between the first few points (with the exception of the outliers). To remove the effect of the outliers and have a more robust estimation I thus decided to use the 5th point in the sorted sequence of the points instead of the minimum one. I decided to use the fifth since it is large enough to remove the few outliers I saw in the data and it was still small enough to be a good first point of collision. To compute the 5th point I simply used the `std::nth_element` standard function.

## FP.3 Associate Keypoint Correspondences with Bounding Boxes

*Prepare the TTC computation based on camera measurements by associating keypoint correspondences to the bounding boxes which enclose them. All matches which satisfy this condition must be added to a vector in the respective bounding box.*

## FP.4 Compute Camera-based TTC

*Compute the time-to-collision in second for all matched 3D objects using only keypoint correspondences from the matched bounding boxes between current and previous frame.*

## FP.5 Performance Evaluation 1

*Find examples where the TTC estimate of the Lidar sensor does not seem plausible. Describe your observations and provide a sound argumentation why you think this happened.*

## FP.6 Performance Evaluation 2

*Run several detector / descriptor combinations and look at the differences in TTC estimation. Find out which methods perform best and also include several examples where camera-based TTC estimation is way off. As with Lidar, describe your observations again and also look into potential reasons.*
