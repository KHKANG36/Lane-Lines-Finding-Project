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

1) Color image to gray #scale  
- I used FCN-8 encoder/decoder architecture. I loaded pretrained VGG16 model into tensorflow followed by 1 by 1 convolution for spartial information. Then, I created the layers for a FCN (Fully Convolutional Network) using deconvolution and skip connection technique. For the detailed undertanding, please refer to below architecture image which I used in this project. 
![Test image](https://github.com/KHKANG36/Semantic-Segmentation/blob/master/FCN%20for%20Semantic%20Seg.gif)

2) Class
- I classified 4 objects in this simulation. (Road - Purple, Vehicle - Blue, Ped - Red, Traffic Light - Yellow)
 
## The Result
1) Cityscape dataset test images
- Mostly, it could pretty much classify most of the objects.
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000000_000019_leftImg8bit.png)
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000037_000019_leftImg8bit.png)
![Test image](https://github.com/KHKANG36/Semantic-Segmentation_Multiple-Class/blob/master/runs/berlin_000061_000019_leftImg8bit.png)

2) Recored road video (Germany)
- I applied the trained model to the real road video. It showed good performance. You can see the full video (semantic_output.mp4) in my repo. 
