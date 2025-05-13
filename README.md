
<!-- by 梁梅-->

# CatraMMS Face Recognition Feature Usage Guide

## Phase 1: Data Preparation  
1. Reference Data Ingestion  
   Objective: Build a facial feature comparison database.  
   Steps:  
     1. Upload reference face images/video clips to the media library via the media management API.

![Upload File](iamges/上传文件.png)  
![Select File](iamges/选择文件.png)  
     3. The system returns a unique identifier medialtemKey (e.g., 11).  
![Return Unique Identifier](iamges/返回唯一标识符.png)  
     4. Annotate metadata with deepLearnedModelTags (e.g., identity label GIULIANO) to link with pre-trained deep learning models.  

2. Input Stream  Registration  
   Objective: Define the video source for recognition.  
   Steps:  
     1. Register the target video stream/file to the system and obtain its configurationLabel (e.g., conf-video-45).  
     2. Validate protocol compatibility (supports RTMP, HLS, HTTP-FLV, etc.).  

## Phase 2: Task Configuration  
Create a Task File:  
![Json code](iamges/人类识别Json代码.png)

## Phase 3: Task Submission & Execution  
1. API Task Submission  
   Objective: Trigger the asynchronous processing pipeline.  
   Steps:  
     1. Call the POST /api/tasks endpoint to submit the task configuration file.  
     2. The system returns an encodingJobKey(e.g., 789) for status tracking.  

2. Task Queue Scheduling  
   System Behavior:  
     1. Tasks enter a distributed queue and are assigned to available compute nodes via load balancing.  
     2. Nodes load pre-trained models (e.g., FaceNet, ResNet) and cascade classifier files (.xml).  

# CatraMMS Live Grid Feature Usage Guide  

## Phase 1: Input Stream Preparation & Registration  
1. Define Input Streams  
   Objective: Specify multi-source live streams and their technical parameters.  
   Steps:  
     1. Register each stream via the stream management API, noting protocol (RTMP/SRT/HLS), resolution, frame rate, and codec.  
     2. Assign unique configurationLabel values (e.g., conf-stream-1, conf-stream-2).  
     3. Validate stream stability (buffering strategies, reconnection) and protocol compatibility.  

2. Encoding Presets  
   Objective: Define output encoding parameters to balance quality and bandwidth.  

## Phase 2: Task Submission & Execution  
1. API Task Submission  
   Objective: Trigger the distributed synthesis pipeline.  
   Steps:  
     1. Submit the task configuration file via POST /api/tasks.  
     2. The system returns an encodingJobKey (e.g., 789) and initial status (queued/running).  

2. Task Scheduling & Resource Allocation  
   System Behavior:  
     1. Tasks enter a priority queue and are assigned to compute nodes with the lowest load.  
     2. Nodes initialize FFmpeg instances, load input streams, and bind filter chains (e.g., xstack or grid filters).  
     3. Hardware acceleration (NVIDIA NVENC/Intel QSV) is enabled for layout synthesis.  

## Phase 3: Core Processing Workflow  
1. Stream Decoding  
   Implementation:  
      Demux input streams via FFmpeg's libavformat to extract raw audio/video data.  
      Apply dynamic buffering (Jitter Buffer) to handle network fluctuations.  

2. Grid Layout Synthesis  
   Filter Chain:  
      Use scale to normalize sub-stream resolutions (e.g., 960x540).  
      Define layouts via xstack (e.g., layout=0_0|w0_0 for horizontal alignment).  

3. Encoding & Streaming  
   Implementation:  
      Encode synthesized video with presets (e.g., h264_nvenc).  
      Push to CDN/media servers via librtmp or libsrt.  

# CatraMMS Live Recording Feature Usage Guide  

## Phase 1: Input Stream Configuration & Registration  
1. Stream Definition & Validation  
   Objective: Ensure stability and compatibility of live streams.  
   Steps:  
     1. Register streams via the stream management API, specifying protocol (RTMP/HLS/SRT), resolution, frame rate, and codec (H.264/H.265).  
     2. Assign a unique configurationLabel (e.g., conf-live-1) for task binding.  
     3. Validate connectivity and configure dynamic buffering (Jitter Buffer).  

2. Storage Path Planning  
   Objective: Define persistent storage locations and retention policies.  
   Steps:  
     1. Configure paths in predefinedEncodingProfiles/storage.json (e.g., /mnt/recordings/ or AWS S3/Aliyun OSS).  
     2. Set retention rules (e.g., retentionDays: 30) and cleanup policies (LRU/time-based).  

## Phase 2: Task Configuration & Initialization  
Example JSON Task File:  
![Json code](iamges/直播录制json代码.png)

## Phase 3: Task Submission & Execution  
1. API Task Submission  
   Objective: Trigger the recording pipeline and allocate resources.  
   Steps:  
     1. Submit the task file via POST /api/tasks to receive an encodingJobKey .  
     2. Tasks are distributed to optimal compute nodes via a scheduler.  

2. Real-Time Stream Processing & Recording  
   Implementation:  
     1. Initialize FFmpeg to demux streams via libavformat.  
     2. Generate segmented files based on rules (time/size) and write to storage.  
     3. Handle interruptions:  
        - Reconnection: Max retries (default 5), timeout threshold (e.g., 10s).  
        - Resume recording from the last valid timestamp.  

## Phase 4: Task Monitoring & Status Management  
1. Real-Time Status Query  
   Response Fields:  
       Task state (running, paused, completed, error).  
       Path of the active segment file.  
       Error details (e.g., stream interruption, storage failure).  
