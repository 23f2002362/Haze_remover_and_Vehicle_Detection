# Problem 
Adverse weather conditions, particularly fog and heavy haze, are a major contributing factor to traffic
accidents worldwide. The reduction in visibility distance makes it extremely difficult for drivers to
perceive other vehicles and obstacles, drastically reducing reaction times. A catastrophic example of
this is the 200-vehicle pileup in central China, which occurred amid thick fog and resulted in a tragic
loss of life. Such incidents highlight the critical need for robust driver assistance systems that can "see"
through the haze and provide early warnings. While advanced sensors like radar and LiDAR can
penetrate fog, their high cost prohibits widespread adoption in consumer vehicles. Therefore,
developing an affordable, vision-only system that can reliably function in these conditions is a
paramount challenge in automotive safety.

![2016_11$largeimg06_Sunday_2016_231552555](https://github.com/user-attachments/assets/4c6c348c-1a15-4666-bab3-e4391924bdc9)
<img width="1907" height="1174" alt="image" src="https://github.com/user-attachments/assets/4b4be299-2cc4-474f-be53-7f4216a25f17" />
Figure 1 - (a) 6 killed, 51 hurt in mishaps due to smog - The Tribune
(b) Dense fog in North India hits air, rail traffic; causes road accidents - Rediff.com

## Proposed solution
We propose a hybrid computer vision pipeline that tackles the challenge in two sequential steps. The
system first ingests a live video feed and applies the Dark Channel Prior (DCP) algorithm to each
frame. This computationally restores image clarity by estimating and removing the atmospheric haze.
The resulting clear, dehazed video stream is then fed into a highly optimized, deep-learning model for
real-time vehicle detection. The detection model, based on YOLOv8n, is trained to identify vehicles
and their orientation, enabling an alarm system to alert the driver to potential collision threats ahead.

## Dark Channel Prior - Dehazing algorithm 
This algorithm takes a single image and dehazes it to achieve a less foggy image
like
<img width="2621" height="1480" alt="image" src="https://github.com/user-attachments/assets/b2d8b847-f553-4328-97b0-6b3c1730106f" />

### Step-1 Calculation of Transmission Map
<img width="2036" height="1320" alt="image" src="https://github.com/user-attachments/assets/1795c88f-156a-4fdf-8150-b4b45324c70c" />

### Step-2 Calculation of Dark Channel Prior  
<img width="2048" height="1326" alt="image" src="https://github.com/user-attachments/assets/2c727a4b-3405-47ad-bc07-d6ac1e4fac86" />
     
### Step-3 Calculation of Estimate Transmission    
<img width="1110" height="721" alt="image" src="https://github.com/user-attachments/assets/d85bda41-40a0-4c7e-ac33-b44935a9b283" />
     
### | To achieve |
<img width="1827" height="1147" alt="image" src="https://github.com/user-attachments/assets/82015ebd-8b00-4f40-a5c7-fb76c668cb6d" />
### Heat Map
<img width="3415" height="2251" alt="image" src="https://github.com/user-attachments/assets/6c795e68-7758-41d3-b0f9-5549073b5ea3" />


## Vehicle detection - Specific Model Training
We trained lightweight CNN YOLOv8n and YOLO11n models, heavyweight CNN yolopv2 (where the GPU device is powerful enough) on 
Vehicle Orientation dataset:- 
https://www.kaggle.com/datasets/raghavdharwal/vehicle-orientation-dataset-part-1

This will help our software to predict vehicles at 6FPS that will alarm the driver

with detection on screen looks like this:- (Yolo PV2)
<img width="3996" height="2251" alt="download (1)" src="https://github.com/user-attachments/assets/787d7c35-cba5-49e4-a8ba-e29533efec82" />








