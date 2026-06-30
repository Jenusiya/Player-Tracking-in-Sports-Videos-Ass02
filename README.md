# Player-Tracking-in-Sports-Videos-Ass02

**Introduction**

This project focuses on developing a computer vision–based system for player detection, tracking, and pose estimation in sports videos. The objective is to analyze short sports clips and automatically detect players, track their movements across frames, and estimate body keypoints using deep learning models.

Two main tasks were implemented: player detection with tracking using a YOLOv8 model and pose estimation using a YOLOv8 pose model.

**Dataset Description**

The dataset consists of short sports video clips stored in Google Drive.

Source: YouTube sports videos
Sports: Football, cricket, and rugby
Duration: 5–10 seconds per clip
Format: MP4 videos
Number of videos: Multiple clips stored in a folder

The videos contain dynamic scenes with multiple moving players, making them suitable for real-world detection and tracking experiments.

**Implementation**
**Environment Setup**

The system was implemented in Google Colab using Python. Required libraries such as OpenCV, PyTorch, and Ultralytics (YOLOv8) were installed. GPU availability was checked to improve processing speed.

Google Drive was mounted to access input videos and store output results.

**Player Detection and Tracking Model**

A pretrained YOLOv8 nano model (yolov8n.pt) was used for player detection. The model was configured to detect only the person class.

To improve analysis over time, object tracking was enabled using ByteTrack. This allowed the system to assign unique IDs to players and follow them across frames.

For each frame:

Players were detected using YOLOv8
Bounding boxes were drawn around each player
Tracking IDs were assigned to maintain identity across frames
Duplicate detections were removed using internal tracking logic

The final output was saved as a tracked video.

**Pose Estimation Model**

A pretrained YOLOv8 pose estimation model (yolov8n-pose.pt) was used for keypoint detection.

This model identifies human body joints such as:

Head
Shoulders
Elbows
Wrists
Hips
Knees
Ankles

These keypoints are connected to form a skeleton representation of each player.

For each frame:

The pose model detects human keypoints
Skeleton structures are drawn on detected players
The annotated frame is saved into an output video

**Output Processing**

Each input video was processed in two stages:

**Tracking Output Generation**
Player detection with bounding boxes
Tracking IDs assigned using ByteTrack
Output saved as tracked_video_i.mp4
**Pose Estimation Output Generation**
Keypoint detection for each player
Skeleton visualization added to frames
Output saved as pose_video_i.mp4

All outputs were stored in Google Drive for evaluation.

**Results and Analysis**

The system was tested on multiple sports videos including football, cricket, and rugby.

**Player Detection and Tracking Results**

The YOLOv8 model successfully detected multiple players in different sports scenarios. In cricket videos, batsmen, bowlers, fielders, and umpires were detected simultaneously. In football and rugby videos, the system detected multiple players even in crowded and fast-moving scenes.

Tracking performance was generally stable, and players were assigned consistent IDs across frames. However, minor identity switches occurred in cases of heavy occlusion or fast movement.

**Pose Estimation Results**

The pose estimation model produced accurate skeleton structures for most detected players. It successfully captured key movements such as bowling actions in cricket and running or passing movements in football and rugby.

Some inaccuracies were observed when players were far from the camera or partially hidden. Despite these limitations, the overall pose estimation results were visually meaningful and consistent.

**Performance Discussion**

Overall, the system performed well in detecting, tracking, and estimating poses of players across different sports environments. The combination of YOLOv8 detection, ByteTrack tracking, and pose estimation provided a strong pipeline for sports video analysis.

However, performance decreased in challenging conditions such as occlusion, low resolution, and fast motion.

Limitations and Improvements
**Limitations**
Reduced accuracy for distant or small players
Tracking instability in crowded scenes
Occlusion affects both detection and pose estimation
Limited dataset size

**Future Improvements**
Use larger YOLOv8 models (s/m/l) for improved accuracy
Replace ByteTrack with advanced tracking methods like BoT-SORT or DeepSORT
Improve pose estimation using temporal smoothing techniques
Train on a larger and more diverse sports dataset
Add long-term player re-identification (Re-ID)


**Conclusion**

This project successfully demonstrates a deep learning–based system for player detection, tracking, and pose estimation in sports videos using YOLOv8 models.

The system is able to automatically analyze sports footage and generate meaningful visual outputs for both movement tracking and body posture analysis. With further improvements, it can be extended to advanced sports analytics applications such as player performance evaluation and tactical analysis.
