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