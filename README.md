# Lane line detection/tracking project (Ver.2)
In this project, I implemented the algorithm which detects lane line on the road based on the computer vision technique. In particular, I used a variety of computer vision techniques and unique algorithms to make it robust. All codes are written on the iPython notebook. 

## Requirement 
- Python 3.0 >
- Numpy
- CV2
  
## Run the Project 
Open the 'Lane_line_detection.ipynb' file and run it sequencially. All required image/video files are uploaded in this project repo.

## Project Implementation
Below is project pipeline used in this project.

**(1) Color image to gray scale → (2) Gaussian bluring → (3) Canny edge detection → (4) Color image to HLS scale and extract H-channel & S-channel → (5) Combine all (H-channel AND S-channel OR Canny edge detection) → (6) Masking with ROI(Region of Interest) → (7) Hough Transform and draw lines** 

**1) Color image to gray scale → Gaussian bluring → Canny edge detection** 

- In order to apply canny edge detection, I converted the color image in gray scale. With gaussian bluring, we can remove noise which hinder to detect the edge correctly. I applied the canny edge detection to blurred gray scale image(Right).
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/DK2.jpg) ![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/edge_detect_result.png)

**2) Color image to HLS scale and extract H-channel & S-channel** 
- When we look at the above "canny edge detection" image, we can recognize that we lost some yellow lane line information in the lighted region. In the below image, we can also see that we lose valuable yellow color information when we convert the image in grayscale.
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/gray_scale_yellowline.png) 

- I converted RGB image to HLS color scale and extract the S-channel and H-channel. As below binary images, we can see that both channel recognize the yellow line well. However, S-channel (left image) is weak for the shadow. Otherwise, H-channel (right image) is weak for the light. Therefore, I merged two channel information with "bitwise_and". After that, I combined it with edge-detected binary image. The combined image can detect both yellow and white line strongly, and eliminate any shadows or bright lights. The bottom image is the combined image result. 

![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/s_channel_result.png)
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/h_channel_result.png) 
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/combined_result.png) 

**3) Masking with ROI (Region of Interest)** 
- I used 4 vertices for the trapezoid masking with ROI : (100,height),(width/2-45,height/2+60),(width/2+45,height/2+60),(width-
50,height). Because the ADAS camera is mounted fixed location (behind the room mirror), the marking region generally works for almost every camera image.  
- Below image is extracted binary image from our ROI(region of interest)
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/masked_result.png)

**4) Hough Tranform** 
- Within the ROI, I extract the lane line candidates via Hough Transform algorithm. Hough transform algorithm returns line starting point(x1,y1) and end point(x2,y2) coordinates of candidates lines. Because lane-line can be distingushed clearly, I used the parameters of Hough transform aggressively in order to extract only distinct lane-line(min_line_length=35, max_line_gap=20). 

**5) Draw lines** 
- After extracting the lane line candidates via Hough transform, I initially calculate the slope of the every line. Then, I averaged the slope and calculate the x,y intercept to draw the one left and one right line. Since the slope of the lane line is within certain boundary, I removed the outlier line (if the slope is too high or too low) when calculating the average.
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/Lanefind_result.png)

**6) Draw lines for video** 
- The location of lane line is not abruptly changed since vehicle is statically driving in most of times. So, I made a tracking algorithm which uses several previous image frames on video and averages the location of lane lines. With this approach, even though we wrongly detect the lane line in one image frame due to the shadows or lights, it would not be much deviated from the original location because the correctly detected information of several previous images would successfully compensate it. If you have chance to see the video (on my github repo), the lane line is not much deviated from the ground truth even in high shadow or light conditions. Rather than that, it is very robust to outside environment and detect the lane line in a very steady way.    

## The Conclusion
- Lane line detection in camera images is very basic functions in self-driving vehicle. However, stable lane line detection is still a difficult issue to be resolved. In this project, I implemented two unique approaches to detect stable lane line. First of all, I used several color channels not only RGB channel but also HLS and HSV channel in order to extract correctly the lane line in a variety of environment. Secondly, I used the tracking algorithm for stable lane line detection for video images. My works here could be the one potential solution for improved detection algorithm. 
