# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## Midterm Project Report

* MP.1 Data Buffer Optimization

A new dataBuffer object is pushed only if size of vector is less than maximum size. Once max size is reached, all vector elements are rotated to the left with first element becoming last element. Then last element is overwritten with the new databuffer

* MP.2 Keypoint Detection

Used OpenCV methods to implement the required detectors. For SHITOMASSI and HARRIS the configuration is provided to the APIs. In case of Modern detectors, the create for the needed detector is used which provide the default configuration parameters for the detector based on its type

* MP.3 Keypoint Removal

Used rectangle contains method to keep only Keypts located inside the rectangle

* MP.4 Keypoint Descriptors

Used OpenCV methods to implement the required descriptors. The method create is used to create the correct descriptor and the method compute is used to compute the descriptor and fill the Mat

* MP.5 Descriptor Matching

Used OpenCV FlannBasedMatcher class to create FLANN matcher. 
Used OpenCV KnnMatch method to implement K-Nearest-Neighbor matching

* MP.6 Descriptor Distance Ratio

Calculated the ratio between nearest and second nearest matches from Knn matcher. If the ratio is more than 0.8 the match is not added to the matches output vector (i.e: excluded)

* MP.7.8.9 Performance Evaluation 1/2/3

Print out the size of KeyPts, the KeyPts on the vehicle and the size of the matches on the vehicle. Print the time for detector and descriptor calculation methods. Use BF approach for matching with distance ration filter. Provide data for all detector/descriptor combination is /doc/ Udacity_Camera2d_ProjectReport.xlsx file


## Midterm Project Performance Evaluation

THe runtime performance is a deceisive factor in Realtime applications like feature tracking in the field of driving assistance and automated driving. Therefore the TOP3 would be:

1. FAST + BRIEF		Avg t = 1.25 ms , Avg match Perc. = 74%

2. FAST + ORB		Avg t = 1.56 ms , Avg match Perc. = 72%

3. FAST + BRISK		Avg t = 2.22 ms , Avg match Perc. = 60%

Avg t (detector time + descriptor time), Avg match percentage (Matched KeyPts / Total KeyPts)
