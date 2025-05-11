##Media Management System

##Media Management System functionalities

-manage "WorkSpaces" for the media contents. Every "Workspace" is a repository of media contents. Example 1: a Workspace could contain all the 'News' contents, another all the 'Sport' contents, ... Example 2: a Workspace could contains all the contents of 'User A', another Workspace could contains all the contents of 'User B', ...
-manage custom workflows (an example of workflow: ingest two videos, concatenate them, cut the resulting video, overlay a logo on it, encode it using different profiles, ...)
-manage libraries of Workflows. For example it is possible to create a workflow to retrieve a Picture from a video. It will be composed by several Tasks, a Task looking for a Face into the Video, if it does not find any face (OnError event), there is another Task getting a Picture at a specified instance (i.e.: 30 seconds since the starting of the Video). Then we have the encoding of the generated picture and so on. All that could be saved as a 'Workflow As Library' and it can be used as a simple Task in other Workflows.
-manage custom metadata associated to each content
-manage CrossReferences among the Media Contents (i.e.: ImageOfVideo, ImageOfAudio, FaceOfVideo, CutOfVideo, CutOfAudio, ...)
-manage an array of Encoders, priority of each encoding and dedicated Encoders for each Workspace
-implement media functionalities (i.e.: encoding, cut (KeyFrameSeeking, FrameAccurateWithoutEncoding and FrameAccurateWithEncoding), -concatenate, overlay, slideShow, video speed down, picture in picture, check streaming for monitoring, ...)
-multi tracks support in any fuctionalities (LiveRecorder, Concat, Cut, ChangeFileFormat, ...)
-multi bitrate support
-integrated with Kaltura
-ngest VOD and Live YouTube contents
-record live IP streaming, even from YouTube
-live Recorder Virtual VOD
-implement a proxy for live IP streaming and Media On Demand toward CDN or making live streaming available through HLS/DASH requests
-Certified CDN: CDN77, AWS
-Live-Grid (Live-Mosaic) to compose/merge several videos in one video (useful for example for monitoring/surveillance)
-manage delivery of contents through the creation of authorizations by path or by parameter (tokens, time to live, max retries)
-post media on socials (facebook, youtube, ...)
-implement computer-vision (face recognition, face identification, ...)
-implement image processing