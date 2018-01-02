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

(1) Color image to gray scale → (2) Gaussian bluring → (3) Canny edge detection → (4) Color image to HLS scale and H-channel & S-channel → (5) Combine all (H-channel AND S-channel OR Canny edge detection) → (6) Masking with ROI(Region of Interest) → (7) Hough Transform and draw lines 

1) Color image to gray scale → Gaussian bluring → Canny edge detection 
- Below is the original image which I tested in my algorithm.  
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/DK2.jpg){: width="100px" height="20px"}
- In order to apply canny edge detection, I converted the color image in gray scale. With gaussian bluring, we can remove noise which hinder to detect the edge correctly. I applied the canny edge detection to blurred gray scale image.
![Test image](https://github.com/KHKANG36/Lane-Lines-Finding-Project/blob/master/sample_images/edge_detect_result.png)

2) Class
- I classified 4 objects in this simulation. (Road - Purple, Vehicle - Blue, Ped - Red, Traffic Light - Yellow)
Gray lose yellow color & canny edge can not detect the yellow 
 
## The Result
1) Cityscape dataset test images
- Mostly, it could pretty much classify most of the objects.
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000000_000019_leftImg8bit.png)
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000037_000019_leftImg8bit.png)
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000061_000019_leftImg8bit.png)

2) Recored road video (Germany)
- I applied the trained model to the real road video. It showed good performance. You can see the full video (semantic_output.mp4) in my repo. 
