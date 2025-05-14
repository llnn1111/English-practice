
<!-- by 韦柔 -->
# Content Encoding Function

![Screenshot of Encoding Function](images/Encoding%20function.png)

## 1. Video Encoding

### 1.1 Function Overview
The video encoding functionality in CatraMMS offers flexible configuration options and supports multiple formats and parameter settings.

### 1.2 User Configuration
The system manages video encoding through preset configuration files and API interfaces. Users can configure parameters including:
- Codec (e.g., libx264)
- Profile (e.g., high422/main)
- Bitrate
- Framerate
- Resolution

### 1.3 Core Implementation
The key functionality is implemented in `API/src/API_Encoding.cpp`, which contains essential functions such as:
- `addEncodingProfile()`
- `removeEncodingProfile()`

![Screenshot 1 of video coding function](images/Video%20encoding1.png)

### 1.4 Predefined Profiles
Predefined video encoding profiles are stored in JSON format under the `predefinedEncodingProfiles/video/` directory.

### 1.5 Supported Formats
The system supports container formats including:
- MP4
- DASH
- TS

With preset bitrate-resolution combinations optimized for various usage scenarios.

![Screenshot 2 of video coding function](images/Video%20encoding2.png)

## 2. Audio Encoding

### 2.1 Module Flexibility
The audio encoding module can operate either as a standalone component or in conjunction with video encoding.

### 2.2 Core Codec
The system adopts AAC as its core audio codec, offering configurable bitrates ranging from 92kbps to 160kbps (e.g., AAC_160 in video encoding profiles).

### 2.3 Profile Storage
Predefined audio encoding profiles are stored in JSON format under `predefinedEncodingProfiles/audio/`.

### 2.4 Advanced Processing
Professional audio processing features include:
- Loudness normalization
- Noise suppression
- Intelligent segmented encoding (particularly suited for podcast and music production)

### 2.5 Multichannel Support
Multi-channel audio support enables processing of professional formats (e.g., 5.1 surround sound), meeting high-standard media production requirements.

![Screenshot of audio coding function](images/Audio%20encoding.png)

## 3. Image Encoding

### 3.1 Core Functionality
The system supports mainstream format conversion with intelligent compression capabilities.

### 3.2 Preset Templates
A preset template named "MMS_JPEG_85Q_1920x1080" is provided, specifying:
- Quality parameters (85Q)
- Resolution settings

### 3.3 Profile Storage
Predefined image encoding profiles are stored in JSON format under `predefinedEncodingProfiles/image/`.

### 3.4 Optimizations
Key optimizations include:
- Progressive loading
- Adaptive format selection (for web)
- Automatic multi-resolution generation (for mobile devices)

### 3.5 Professional Features
The image processing engine supports:
- Metadata retention
- Automatic orientation correction
- Batch processing of bulk image files

Significantly enhancing content management efficiency.

![Screenshot of audio coding function](images/Image%20encoding.png)

# Notification Function

The notification function in Catramms primarily facilitates communication between users and the system support team via email.

As shown in the operation interface screenshot, the system provides a simple form that requires users to fill in:
- Email address
- Subject line
- Message content

With support for sending emails to specified mailboxes.

## Implementation Components
1. The frontend interface collects the email information entered by the user
2. The backend processing logic handles the actual email transmission
3. The system uses the SMTP protocol to communicate with the mail server

![Screenshot of audio coding function](images/Notification%20function.png)

# Security

## 1. Identity Authentication  
The CatraMMS project verifies user identities through email, passwords, and other methods to ensure only authorized users can access the system.  
The user registration and confirmation process strictly controls the legitimacy of user identities.  

For example, the `confirmRegistration` function: This function confirms user registration information, and only verified users can officially use the system, further enhancing security. 

![Screenshot of authentication](images/Authentication.png)

## 2. Permission Management  
The system restricts access and operations on media content based on user roles and permissions.  
Users with different roles have varying permissions, ensuring only authorized users can perform specific actions.  

In the `createWorkspace` function within the `CatraMMS/API/src/API_UserWorkspace.cpp` file, user permissions are checked to determine whether a workspace can be created.  

## 3. Data Encryption  
- The project encrypts media content stored in the system to prevent data theft during storage.  
- SSL/TLS and other encryption protocols are used during media content transmission to ensure secure data transfer.  

## 4. Logging and Auditing  
- The project logs critical system operations and access records to support auditing and tracing in case of security incidents.  
- Detailed logs help detect and address abnormal operations promptly.  

`SPDLOG_INFO` and `SPDLOG_ERROR` macros: These are used in multiple files, such as `CatraMMS/API/src/API_UserWorkspace.cpp`, to record system-critical information and errors, facilitating subsequent auditing and tracing.  
<!-- by 韦柔 -->



<!-- by 梁梅-->

# CatraMMS Face Recognition Feature Usage Guide

## Phase 1: Data Preparation  
1. Reference Data Ingestion  
   Objective: Build a facial feature comparison database.  
   Steps:  
     1. Upload reference face images/video clips to the media library via the media management API.
![Upload File](/iamge/点击上传文件按钮.png)
![Select File](/iamge/选择上传文件.png)  
     3. The system returns a unique identifier medialtemKey (e.g., 11).
![Return Unique Identifier](/iamge/返回唯一标识符.png)  
     5. Annotate metadata with deepLearnedModelTags (e.g., identity label GIULIANO) to link with pre-trained deep learning models.  

2. Input Stream  Registration  
   Objective: Define the video source for recognition.  
   Steps:  
     1. Register the target video stream/file to the system and obtain its configurationLabel (e.g., conf-video-45).  
     2. Validate protocol compatibility (supports RTMP, HLS, HTTP-FLV, etc.).  

## Phase 2: Task Configuration  
Create a Task File:  
![Json code](/iamge/人脸识别任务Json代码.png)

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
![Json code](/iamge/直播录制json代码.png)

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

# English Practice
## Features

## Content Ingestion Functionality <!-- by Long Qingting -->

CatraMMS provides a flexible content ingestion pipeline supporting multiple ingestion methods:

1. **Local File Upload**
    Users can upload local files through a simple file picker interface. The script example at `CatraMMS/scripts/examples/ingestOfImage/helper/ingestionWorkflow.sh` demonstrates this operation, requiring users to configure:
    - User/API keys for authentication
    - Metadata (title, tags, retention policy)
    - File format validation

    Command example:
    ```bash
    if [ $# -ne 8 ]; then
    echo "Usage: $0 <mmsUserKey> <mmsAPIKey> <title> <tag> <ingester> <profileset> <retention> <fileFormat> ($#)"
    exit 1
    fi

    mmsAPIHostName=mms-api.cibortv-mms.com
    mmsUserKey=$1
    mmsAPIKey=$2
    title=$3
    tag=$4
    ingester=$5
    profileSet=$6
    retention=$7
    fileFormat=$8

    sed "s/\${title}/$title/g" ./helper/ingestionWorkflow.json | sed "s/\${tag}/$tag/g" | sed "s/\${ingester}/$ingester/g" | sed "s/\${profileSet}/$profileSet/g" | sed "s/\${retention}/$retention/g" | sed "s/\${fileFormat}/$fileFormat/g" > ./helper/ingestionWorkflow.json.new

    responseCode=$(curl -o ./helper/ingestionWorkflowResult.json -w "%{response_code}" -k -s -X POST -u $mmsUserKey:$mmsAPIKey -d @./helper/ingestionWorkflow.json.new -H "Content-Type: application/json" https://$mmsAPIHostName/catramms/1.0.1/workflow)
    if [ "$responseCode" -ne "201" ]; then
             echo "$(date +%Y-%m-%d-%H:%M:%S): FAILURE, Ingestion response code: $responseCode"
             exit 2
    fi

    rm ./helper/ingestionWorkflow.json.new

    #print ingestionJobKey
    jq '.tasks[] | select(.type == "Add-Content") | .ingestionJobKey' ./helper/ingestionWorkflowResult.json
![alt text](images/图像上传.png)
![alt text](images/视频上传.png)


2. **Cloud Storage Integration**
    Supports direct content import from third-party cloud providers (e.g., Google Drive, Dropbox) via sourceURL configuration. While no specific cloud SDKs are used, the system supports fetching content from external storage URLs:

    ```json
    "parameters": {
           "sourceURL": "http://myhost/example.mp4",  // Supports HTTP/HTTPS/FTP/FTPS protocols
           // ...
    }


3. **Batch Import**
    Allows users to import multiple files at once, supporting various file formats. The script at CatraMMS/scripts/examples/ingestionOfStreamingURL/ingestionOfStreamingURL.sh demonstrates batch import by processing files containing multiple titles and streaming URLs sequentially:

    ```bash
    if [ $# -lt 8 ]; then
            echo "Usage: $0 <mmsUserKey> <mmsAPIKey> <tag> <ingester> <retention> <encodersPool> <encodingProfilesSet> <streamingURLFile>"
            echo "The current parameters number is: $#, it shall be 9"
            paramIndex=1
            for param in "$@"
            do
                echo "Param #$paramIndex: $param";
                paramIndex=$((paramIndex + 1));
            done
            exit 1
    fi

    mmsUserKey=$1
    mmsAPIKey=$2
    tag=$3
    ingester=$4
    retention=$5
    encodersPool=$6
    encodingProfilesSet=$7
    streamingURLFile=$8

    mmsAPIHostName=mms-api.catramms-cloud.com

    while read titleAndtreamingURL; do
            if [ "$titleAndtreamingURL" = "" ]; then
                continue
            fi

    title=$(echo $titleAndtreamingURL | cut -d ";" -f 1)
    streamingURL=$(echo $titleAndtreamingURL | cut -d ";" -f 2)
    encodedStreamingURL=${streamingURL//\//"\\/"}
    encodedStreamingURL=${encodedStreamingURL//\&/"\\&"}

    sed "s/\${title}/$title/g" ./helper/ingestionWorkflow.json | sed "s/\${streamingURL}/$encodedStreamingURL/g" | sed "s/\${tag}/$tag/g" | sed "s/\${ingester}/$ingester/g" | sed "s/\${retention}/$retention/g" | sed "s/\${encodersPool}/$encodersPool/g" | sed "s/\${encodingProfilesSet}/$encodingProfilesSet/g" > ./helper/ingestionWorkflow.json.new
    curl -o ./helper/ingestionWorkflowResult.json -k -s -X POST -u $mmsUserKey:$mmsAPIKey -d @./helper/ingestionWorkflow.json.new -H "Content-Type: application/json" https://$mmsAPIHostName/catramms/1.0.1/workflow
    done < "$streamingURLFile"
![alt text](images/批量上传.png)
        

4. **Automated Ingestion**
    Implements scheduled ingestion through:

    Filesystem monitoring: Initially designed using incrontab (inotify-based), later adapted to use cron-triggered scripts due to mounted directory limitations
    Watch folder pattern: Periodically scans designated directories for new files



## Content Handling Capability <!-- by Long Qingting -->

1. **Multimedia Format Transcoding**
    The system provides professional media transcoding services, supporting conversion between various video container formats, including but not limited to transcoding source files into standardized container formats such as MP4 and AVI. In the CatraMMS/API/src/FFMPEGEncoderTask.cpp implementation, the downloadMediaFromMMS function establishes a complete transcoding pipeline, specifically designed to handle the download and transcoding process of streaming media content based on the HLS protocol, efficiently converting .m3u8 playlist format streaming content into industry-standard MP4 container format.

    ```cpp
    string FFMPEGEncoderTask::downloadMediaFromMMS(
           int64_t ingestionJobKey, int64_t encodingJobKey, shared_ptr<FFMpegWrapper> ffmpeg, string sourceFileExtension, string sourcePhysicalDeliveryURL,
           string destAssetPathName
    )
    {
           string localDestAssetPathName = destAssetPathName;
           bool isSourceStreaming = false;
           if (sourceFileExtension == ".m3u8")
             isSourceStreaming = true;

    if (isSourceStreaming)
    {
            bool regenerateTimestamps = false;
            localDestAssetPathName = localDestAssetPathName + ".mp4";
            ffmpeg->streamingToFile(ingestionJobKey, regenerateTimestamps, sourcePhysicalDeliveryURL, localDestAssetPathName);
    }
    else
    {
            FFMpegProgressData progressData;
            progressData._ingestionJobKey = ingestionJobKey;
            progressData._lastTimeProgressUpdate = chrono::system_clock::now();
            progressData._lastPercentageUpdated = -1.0;

            CurlWrapper::downloadFile(
                sourcePhysicalDeliveryURL, localDestAssetPathName, progressDownloadCallback2, &progressData, 500,
                std::format(", ingestionJobKey: {}", ingestionJobKey),
                3 // maxRetryNumber
            );
    }

    return localDestAssetPathName;
    }
![alt text](images/格式转换.png)

2. **Media File Compression**
    Allowing users to employ codecs for performing lossy/lossless compression on image (JPEG/PNG) and video (H.264/HEVC) files, significantly reducing bitrate and file size. Although the current codebase does not explicitly contain compression algorithm implementations, the system leverages the FFmpeg multimedia framework, utilizing its built-in libx264/libx265 encoders, CRF (Constant Rate Factor) quality control parameters, and preset systems to achieve efficient transcoding workflows. Developers can optimize rate-distortion (R-D) performance by adjusting quantization parameters (QP), GOP (Group of Pictures) structure, and other professional video encoding parameters.

    Take general compression (H.264 + AAC, balancing image quality and file size) as an example:

    ```bash
    ffmpeg -i Guangwai.mp4 -c:v libx264 -crf 23 -preset medium -c:a aac -b:a 128k Guangwai_compressed.mp4

3. **Metadata Extraction**
    The system automatically extracts file metadata (e.g., title, author, creation date) and stores it in a database to facilitate subsequent management and retrieval. In the buildAddContentIngestionWorkflow function located in CatraMMS/API/src/FFMPEGEncoderTask.cpp, the system processes JSON objects containing metadata. The extracted metadata can be stored within these objects, enabling efficient content management and querying capabilities.
    ```cpp
    string FFMPEGEncoderTask::buildAddContentIngestionWorkflow(
            int64_t ingestionJobKey, string label, string fileFormat, string ingester,
            string sourceURL, string title, json userDataRoot,
            json ingestedParametersRoot, int64_t encodingProfileKey,
            int64_t variantOfMediaItemKey
    )
    {
            json addContentRoot;
            string field = "label";
            addContentRoot[field] = label;
            field = "type";
            addContentRoot[field] = "Add-Content";

            son addContentParametersRoot;

            // ... 处理元数据相关逻辑

            if (userDataRoot != nullptr)
            {
            field = "userData";
            addContentParametersRoot[field] = userDataRoot;
            }

            // ...

            return JSONUtils::toString(workflowRoot);
    }

4. **Batch Processing**
    Supports simultaneous processing of multiple files to enhance workflow efficiency. Integrated with the aforementioned batch import functionality, after importing multiple files, users can perform batch operations such as format conversion, compression, and metadata extraction. Leveraging scripting loops and concurrency mechanisms, the system enables parallel processing of multiple files. For instance, in CatraMMS/scripts/examples/ingestionOfStreamingURL/ingestionOfStreamingURL.sh, the script reads a file containing multiple content entries and sequentially ingests and processes each item, significantly improving overall operational efficiency.





<!--by 罗娜-->
Media Management System

Media Management System functionalities

1.manage "WorkSpaces" for the media contents. Every "Workspace" is a repository of media contents. Example 1: a Workspace could contain all the 'News' contents, another all the 'Sport' contents, ... Example 2: a Workspace could contains all the contents of 'User A', another Workspace could contains all the contents of 'User B', ...

2.manage custom workflows (an example of workflow: ingest two videos, concatenate them, cut the resulting video, overlay a logo on it, encode it using different profiles, ...)

3.manage libraries of Workflows. For example it is possible to create a workflow to retrieve a Picture from a video. It will be composed by several Tasks, a Task looking for a Face into the Video, if it does not find any face (OnError event), there is another Task getting a Picture at a specified instance (i.e.: 30 seconds since the starting of the Video). Then we have the encoding of the generated picture and so on. All that could be saved as a 'Workflow As Library' and it can be used as a simple Task in other Workflows.

4.manage custom metadata associated to each content

5.manage CrossReferences among the Media Contents (i.e.: ImageOfVideo, ImageOfAudio, FaceOfVideo, CutOfVideo, CutOfAudio, ...)

6.manage an array of Encoders, priority of each encoding and dedicated Encoders for each Workspace

7.implement media functionalities (i.e.: encoding, cut (KeyFrameSeeking, FrameAccurateWithoutEncoding and FrameAccurateWithEncoding),

8.concatenate, overlay, slideShow, video speed down, picture in picture, check streaming for monitoring, ...)

9.multi tracks support in any fuctionalities (LiveRecorder, Concat, Cut, ChangeFileFormat, ...)

10.multi bitrate support

11.integrated with Kaltura

12.ngest VOD and Live YouTube contents

13.record live IP streaming, even from YouTube
       
14.live Recorder Virtual VOD

15.implement a proxy for live IP streaming and Media On Demand toward CDN or making live streaming available through HLS/DASH requests

16.Certified CDN: CDN77, AWS

17.Live-Grid (Live-Mosaic) to compose/merge several videos in one video (useful for example for monitoring/surveillance)

18.manage delivery of contents through the creation of authorizations by path or by parameter (tokens, time to live, max retries)

19.post media on socials (facebook, youtube, ...)

20.implement computer-vision (face recognition, face identification, ...)

21.implement image processing

22.player
(1).edit video through user mark in-out. Once a cut is done, in case the cut is not accurate, it is possible easily to tune the cut to improve it. 

(2).edit audio through user mark in-out. Once a cut is done, in case the cut is not accurate, it is possible easily to tune the cut to improve it.

(3).edit image cropping through user selection. Once a crop is done, in case the crop is not accurate, it is possible easily to tune the cut to improve it.

23.library available (actually only a java version is available)
(1).to call easily any MMS REST API

(2).to help building by a program any complex Workflow

(3).support for ldap integration (if needed)

24.Media content might be a video, an audio, an image, a playlist.

25.It is designed to be used as a Service where a User has to register first and then will be able to use all the features of the platform. Once a User is registered, a Workspace is created for him and all the created contents will be associated to the Workspace.

26.Currently CatraMMS is using FFMpeg to encode the contents, ImageMagick and opencv for image processing and computer vision functionalities.

27.CatraMMS provides a detailed REST APIs from which it is possible to do any kind of activity toward the platform. Even a GUI/APP can be built based on the APIs.



    Here follow a presentation of the MMS and the Physical Architecture of the CatraMMS:

      

            ┌─────────────┐
            │    End User │
            └──────┬───────┘
                   │
            ┌──────▼───────┐
            │  User By API │
            └──────┬───────┘
                   │
            ┌──────▼───────┐
            │     GUI      │
            └──────┬───────┘
                   │
            ┌──────▼───────┐
            │  Client APP  │
            └──────┬───────┘
                   │
            ┌──────▼───────┐   ┌────────────────┐
            │ Transcoder   │   │  MMS Engine    │
            │   Servers    │   │    Servers     │
            └──────┬───────┘   └────────┬───────┘
                   │                    │
            ┌──────▼───────┐   ┌────────▼───────┐
            │    API       │   │   Clone tt     │
            │   Servers    │   │   https        │
            └──────────────┘   └────────────────┘


Key System Features

MMS is a fully-featured, highly flexible media management platform that covers the entire lifecycle from ingestion, processing, and analysis to distribution. It is particularly suitable for enterprises or developers handling large-scale media resources. Its core advantages include:

(1)Modular Design: Workspaces, workflows, and APIs can all be customized as needed.

(2)Intelligence & Automation: Enhances efficiency by combining AI and rule-based engines.

(3)Open Integration: Supports deep customization through REST APIs and Java libraries.

<!--by 罗娜-->



<!--by 韦淑静-->

Tutorial for Using the Main Functions of a Media Management System

Special Effects Processing Function

(1) Picture Overlay on Video Implementation Logic: This is implemented by defining a task chain in the workflow configuration file. In the file, specify the GroupOfTasks type and nest the Add-Content subtask to load the video source. Then employ FFmpeg or other professional video processing libraries to configure overlay parameters, enabling precise picture overlay.
Application Scenarios: It is widely used in advertising production (e.g., embedding brand logos) and film post - production (e.g., adding atmospheric effect layers).
Operational Steps:
Material Preparation: Prepare the pictures to be overlaid and the target video files.
Configuration File Writing: Define task types and parameters (e.g., overlay position, transparency, etc.).
Task Execution: Submit the configuration file and the system will automatically synthesize the effects.
The operation is as shown below: Prepare the video file and the pictures to be overlaid. Select the workflow editor on the interface (refer to the following illustration).

![图片叠加至视频](</iamges/picture overlay  video-01.png>)


In the workflow, add the necessary subtasks. The functions are visible in the left - hand task library panel (as shown below). Add the subtask for picture overlay on video, specify the task type and parameters, and save the properties.

![图片叠加至视频](</iamges/picture overlay  video-02.png>)
![图片叠加至视频](</iamges/picture overlay  video-03.png>)

<!--by 韦淑静-->


(2) Slideshow Creation Implementation Logic: This involves integrating video frame processing and splicing functions. Multiple images or video clips are sequenced, and a smooth slideshow video is generated by customizing the duration of each material.
Application Scenarios: Suitable for teaching videos, product showcases, event recaps, etc., it supports the orderly presentation of multiple materials.
Operational Steps:
Material Collection: Organize and sort the images or video clips.
Parameter Configuration: Define the material sequence, playback duration, and transition effects in the configuration file.
Task Execution: Submit the configuration for automatic slideshow video generation by the system.
Operation is as shown below: Add the slideshow function subtask in the left - hand task library panel. Then define the material sequence and playback duration parameters, and save the properties.

![制作幻灯片](</iamges/make slides-01.png>)
![制作幻灯片](</iamges/make slides-02.png>)

<!--by 韦淑静-->


Video Speed Adjustment Function: Video Acceleration or Deceleration

Implementation Logic: This function is developed based on the MMSEngine module and relies on FFmpeg and other professional video processing libraries. The core principle involves adjusting the playback speed by modifying the video frame rate or recalculating timestamps. Increasing the frame rate speeds up the video, while decreasing it slows down the video.
Application Scenarios: In film editing, video acceleration can be used to quickly transition between scenes and create a tense atmosphere, whereas deceleration can highlight details. In sports analysis, slowing down video footage of athletes' movements allows professionals to analyze techniques frame by frame, thereby enhancing the effectiveness of training.

Operational Steps:
Material Preparation: Identify the video file that requires speed adjustment and ensure its format is compatible.
Configuration File Creation: Add a "video speed adjustment" task node in the configuration file and set the speed parameters (e.g., 2x acceleration, 0.5x deceleration).
Task Execution: Submit the configuration file to the system for automatic speed adjustment and generation of the target video.

Operation is as shown below: Add a video speed adjustment subtask in the left - hand task library panel, select the speed type and value, and save the properties.

![视频速度调整](</iamges/video speed-01.png>)
![视频速度调整](</iamges/video speed-02.png>)

Connect all subtasks to build a simple workflow and execute it (operation is as shown below).

![工作流子任务配置](/iamges/工作流配置步骤-01.png)
![工作流子任务配置](/iamges/工作流配置步骤-02.png)

After executing the workflow, the platform page displays the corresponding JSON document, showing all added subtasks.

![工作流子任务配置](/iamges/工作流配置步骤-03.png)
![工作流子任务配置](/iamges/工作流配置步骤-04.png)
![工作流子任务配置](/iamges/工作流配置步骤-05.png)

Finally, we can verify whether the workflow executed earlier was successful. Return to the homepage, click the "settings" icon in the upper right corner of the video, select the relevant workflow, and the system will automatically match the workflow name. Then, click the list icon and select "details" to clearly view the subtasks just added, including picture overlay on video, slideshow creation, and video acceleration. Finally, I need to review the entire content to check for any omissions or adjustments needed, ensuring its professionalism and smoothness, and then prepare to formally reply to the user.

![工作流子任务配置](/iamges/工作流配置步骤-06.png)
![工作流子任务配置](/iamges/工作流配置步骤-07.png)
![工作流子任务配置](/iamges/工作流配置步骤-08.png)
![工作流子任务配置](/iamges/工作流配置步骤-09.png)

<!--by 韦淑静-->


Other Functions

(1) File Storage Management
Function Implementation: File storage management encompasses file ingestion and storage path management. File ingestion is accomplished through the Add - Content task within the workflow configuration.
Function Value: It ensures precise file ingestion, efficient storage, and proper organization, thereby enhancing file management efficiency and simplifying subsequent retrieval, usage, and maintenance. In video processing scenarios, it facilitates the proper storage of video files and related resources, ensuring smooth editing and encoding processes.

(2) Workflow Management
Function Implementation: Workflow management is based on workflow configuration files and supporting processing functions. The configuration file, in JSON format, clearly defines essential information such as workflow type, task content, and parameter settings.
Function Value: It enables automated and coordinated system task processing. By defining workflows, related tasks can be combined in a set order and rules, improving work efficiency and accuracy. In a video processing system, workflows covering tasks like video uploading, encoding, and special - effects addition can be created, allowing the system to automatically complete the entire process according to the configuration.

(3) System Configuration Management
Function Implementation: System configuration management involves various configurations, including databases and encoding priorities. At the code level, flexible configuration management is achieved using JSON configuration files and database operations.
Function Value: It enables customized system configuration based on different requirements and environments. By adjusting parameters, system behavior and performance can be optimized, and its adaptability can be enhanced. In a video processing system, encoding priorities can be configured according to video quality requirements to meet diverse user needs.


<!--by 韦淑静-->


<!--by 覃嘉茵-->
Project Overview
Provide a brief introduction to the project. For example:

This project is a Node.js-based frontend application designed to deliver an efficient user interface and features. It utilizes modern frontend tools and frameworks, supporting rapid development and deployment. This document provides step-by-step instructions to set up the environment, verify Node.js installation, and run the frontend application of the Insurance Management System.Node.js is a JavaScript runtime environment based on the Chrome V8 engine, used for building fast and scalable network applications.

Prerequisites
Before starting, ensure your environment meets the following requirements:

Node.js: Version 14.x or higher (LTS version recommended)
npm: Version 6.x or higher (npm comes bundled with Node.js)
Installation and Setup
1. Clone the Repository
First, clone the project code to your local machine:

bash
git clone https://github.com/<YourGitHubUsername>/<ProjectName>.git
cd <ProjectName>

2. Install Dependencies
Run the following command to install all necessary dependencies:

bash
npm install

3. Start the Development Server
Use the following command to start the local development server:

bash
npm start

Once started, you can access the application by visiting http://localhost:3000 in your browser.

Build and Deployment
Build for Production
Run the following command to generate production-ready static assets:

bash
npm run build

The generated files will be stored in the build directory, which can be used for deployment in a production environment.

Deployment
Deploy the contents of the build directory to your server or hosting platform, such as:

GitHub Pages
Vercel
Netlify
Project Structure
Provide an overview of the project’s file structure. For example:

Code
├── src/               # Source code directory
│   ├── components/    # Reusable components
│   ├── pages/         # Page components
│   ├── assets/        # Static assets (images, styles, etc.)
│   └── index.js       # Application entry point
├── public/            # Public files directory
├── package.json       # Node.js project configuration file
└── README.md          # Project documentation
Contribution Guidelines
We welcome contributions to this project! Please follow these steps:

Fork this repository.
Create a new branch: git checkout -b feature-xxx.
Commit your changes: git commit -m "Add xxx feature".
Push the branch: git push origin feature-xxx.
Submit a Pull Request.

 <!--by 覃嘉茵-->


<!--by 卢艳萍-->
1. Project Structure Analysis
1.1
Code-related directories: The directories API/src, MMSEngine/src, and MMSEngineService/src store the core code of the project, which involves the implementation of application programming interfaces, the media management engine, and its services respectively.
1.2
Configuration directory: The conf directory stores configuration files, such as the configuration related to the retention for ingestion jobs. These configurations need to be modified according to actual needs during the installation and deployment process.
1.3
Document-related directories: The docs and generateHtmlDoc directories are related to the project documents. The documents in the docs directory contain detailed descriptions of the project and can be used as a reference during the installation and deployment process.
1.4
Script directory: The scripts in the scripts directory are used to assist in operations such as installation, startup, and stopping of the project. For example, the script update records of IntroOverlay. It is speculated that the scripts play a key role during the project operation. The scripts in the prepareToDeploy directory are also related to deployment.
1.5
Test directory: The stressTest directory is used for stress testing. After the deployment is completed, the test tools in this directory can be used to conduct performance testing on the project.
2. Speculation on Installation and Deployment Steps
2.1
Environment preparation: Since the project is written in C++, a C++ development environment needs to be installed, including compilers (such as GCC or Clang) and build tools (such as CMake). In addition, other libraries on which the project depends need to be installed.
2.2
Obtain the project code: Use the Git command to clone the project code to the local machine. In the terminal, execute git clone https://github.com/giulianoc/CatraMMS.git to download the project code to the local directory.
2.3
Handle submodules: The project contains a.gitmodules file, and there may be submodules. Execute the git submodule init and git submodule update commands to initialize and update the submodules to ensure that all the code on which the project depends is obtained.
2.4
Build the project: Enter the project root directory, create a build directory, and then enter this directory. Execute the cmake.. command to generate build scripts according to the CMakeLists.txt file of the project, and then execute the make command to build the project.
2.5
Configure the project: Modify the configuration files in the conf directory. Set the retention time for ingestion jobs, configure the database connection information, set the storage path for media files, etc.
2.6
Deploy the project: The project includes the server side and the client side, which need to be deployed separately. For the server side, the executable file generated by the build needs to be deployed to the server and the server environment needs to be configured. For the client side, it needs to be deployed to the Web server and ensure normal communication with the server side.
2.7
Test the project: Use the tools in the stressTest directory to conduct stress testing on the project to check the performance and stability of the project under high load. At the same time, conduct functional testing to ensure that functions such as ingestion, processing, encoding, and delivery of the project work properly. In the actual installation and deployment process, the Wiki page of the project (https://github.com/giulianoc/CatraMMS/wiki ) must be referred to in order to obtain more accurate and detailed installation and deployment guidelines.
3. Technology Stack
Backend: Django framework (Python)
Frontend: Bootstrap, jQuery
Database: PostgreSQL
Cache: Redis
Deployment: Docker
4. Dependency Installation
bash
Ubuntu/Debian
sudo apt-get update
sudo apt-get install python3 python3-pip python3-venv postgresql postgresql-contrib redis-server
5. Specific Installation Steps of the Project
5.1 Clone the Code Repository
git clone https://github.com/giulianoc/CatraMMS.git
cd CatraMMS
5.2 Create a Virtual Environment and Install Dependencies
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
5.3 Database Configuration
Create a PostgreSQL user and database
sudo -u postgres psql
CREATE DATABASE catramms_db;
CREATE USER catramms_user WITH PASSWORD '40335';
ALTER ROLE catramms_user SET client_encoding TO 'utf8';
ALTER ROLE catramms_user SET default_transaction_isolation TO'read committed';
ALTER ROLE catramms_user SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE catramms_db TO catramms_user;
5. Configure Environment Variables
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
5.5 Database Configuration
DB_NAME=catramms_db
DB_USER=catramms_user
DB_PASSWORD=40335
DB_HOST=localhost
DB_PORT=5432
5.6 Execute Database Migrations
python manage.py makemigrations
python manage.py migrate
5.7 Collect Static Files
python manage.py collectstatic
python manage.py runserver
Visit http://127.0.0.1:8000/
Production Environment Deployment (Gunicorn + Nginx)
5.8 Configure Nginx
Create /etc/nginx/sites-available/catramms:

nginx
server {
listen 80;
server_name your_domain_or_ip;

location = /favicon.ico { access_log off; log_not_found off; }
location /static/ {
root /path/to/CatraMMS;
}

location / {
include proxy_params;
proxy_pass http://unix:/path/to/CatraMMS/catramms.sock;
}
}
5.9 Enable the Site and Restart Nginx:
sudo ln -s /etc/nginx/sites-available/catramms /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx
5.10 Install Docker and Docker Compose
sudo apt-get install docker.io docker-compose
5.11 Build and Run the Containers
docker-compose up -d --build
Testing and Verification
Visit http://your_domain_or_ip/admin to log in to the management interface and verify functions such as user management, patient entry, and appointment.
Check the log files to troubleshoot problems: /var/log/nginx/error.log and the Django application logs.
Update the Code
git pull origin master
Install New Dependencies
pip install -r requirements.txt
Execute Database Migrations
python manage.py migrate
Collect Static Files
python manage.py collectstatic
Restart the Service
sudo systemctl restart catramms
sudo systemctl restart nginx
<!--by 卢艳萍-->