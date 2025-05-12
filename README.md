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

   <!--by 罗娜-->

    Here follow a presentation of the MMS and the Physical Architecture of the CatraMMS:

        [End User]
        ↓ (use)
        [GUI] → [MMS Engine] ← [API Servers] ← [User By API/Client APP]
        ↓ (if transcoding is required)
        [Transcoder]
        ↑ (return results)
        [MMS Engine] → [GUI/API Servers] → User

<!--by 罗娜-->

    Key System Features
        MMS is a fully-featured, highly flexible media management platform that covers the entire lifecycle from ingestion, processing, and analysis to distribution. It is particularly suitable for enterprises or developers handling large-scale media resources. Its core advantages include:
        （1）Modular Design: Workspaces, workflows, and APIs can all be customized as needed.
        （2）Intelligence & Automation: Enhances efficiency by combining AI and rule-based engines.
        （3）Open Integration: Supports deep customization through REST APIs and Java libraries.

<!--by 罗娜-->


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