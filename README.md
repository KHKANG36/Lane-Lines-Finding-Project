# **Identified lane lines on the road image and video stream**

This is a project for Udacity Self-Driving Car Nanodegree program. In this project I detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images. The implementation of the project is in the file `Project1_Code_RyanKang.ipynb`. 

## Requirement 

- Python > 3.5.0
- OpenCV Library 

## Run the Project 

Prepare test image and video of road which includes the lane line. Otherwise, You can use sample videos uploaded with project files.
Run the `Project1_Code_RyanKang.ipynb` on the ipython notebook. Please modify the image/video source link if you use your own image and video  


## About the Project 

In my pipeline, I converted the images to grayscale initially. Then, I smoothed the converted image to reduce unnecessary noise. After that, I acquired x,y coordinates of image edges by applying "Canny edge detection" algorithm. To apply better region of interests, I analyzed the location of lane-lines for all the images/videos and found optimal 4 vertices based on the height and width information of the images. In order to draw a single line on the left and right lanes, I implemented the draw_lines() function followed by below steps. 1) I separated left and right lane-lines based on the slope of edge-detected lines. If slope > 0, we can guess it right lane. Otherwise, if slope < 0, we can guess it left lane. However, if the value of slope is too small, it might not be a lane-line and might be wrong-detected information. Therefore, I used "0.3" value for lane judgement to increase the correctness. 2) I set Y_max height of the image and found Y_min by comparing all y values. 3) I calculated average slope and average y-intercept of left and right lane each. 4) Based on all information (average slope, y_min, y_max and average y-intercept), I was able to find the x_min, x_max value as well. 5) I Drawed the straight-line with x_min, y_min, x_max, y_max. This is the result of the pipeline on the image:  
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/examples/Test_image1.png)

## Discussion 

1)Potential shortcoming would be the accuracy of the region of interets. Location of the lane could be different with vehicle location or road environment/curve. So, it is inevitable that there should be an error of region of interests even though the location of fixed camera is almost same. We should come up with algorithms which can adopt the region of interest to different image/video intelligently. 2)Another shortcoming could be the accuracy of average slope and average y-intercept. Averaging would not be optimal solution to estimate the optimal slope and y-intercept. So, I tried to optimize the values by using "GradientDecentOptimizer" with tensorflow library. Even though it does not work well, eventually learning based regression algorithm would be useful for this project. 3)The parameter selection for Canny & Hough algorithm was not perfect. 4) When it comes to last "challenge" video, my pipeline didn't work well. The drawed line was not stable because of the sharply curved lane images in video clip.
