# **Identified lane lines on the road image and video stream**

This is a project for Udacity Self-Driving Car Nanodegree program. In this project I detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images. The implementation of the project is in the file `Project1_Code_RyanKang.ipynb`. 

## Requirement 

- Python > 3.5.0
- OpenCV Library 

## Run the Project 

Prepare test image and video of road which includes the lane line. Otherwise, You can use sample videos uploaded with project files.
Run the `Project1_Code_RyanKang.ipynb` on the ipython notebook. Please modify the image/video source link if you use your own image and video  


## About the Project 

To detect the lane line and draw line on the image/video, below steps was implemented: 

1. Convert the images to grayscale
2. Smooth the converted image to reduce unnecessary noise
3. Acquire x,y coordinates of image edges by applying "Canny edge detection" algorithm
4. Apply trapezoid region of interests(ROI) to remove unnecessary image parts 
5. Draw a single line on the detected left and right lanes (Refer to algorithm of draw_lines() function)  

This is the result of the pipeline on the image:  
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/examples/Test_image1.png)

## Discussion/Issues 

1. Accuracy of the region of interests. How can adopt the region of interest to different image/video intelligently? 
2. The optimal parameter selection for Canny edge detection & Hough algorithm
3. Unstable lane line for "challengable" video which has sharp curve, lots of shadow, road pavement and so on.
