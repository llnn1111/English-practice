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

## 1. Authentication and Authorization
- Authenticate users through email, password, etc., to ensure only authorized users can access the system
- Restrict access and operations on media content based on user roles and permissions

![Screenshot of authentication](images/Authentication.png)

## 2. Data Encryption
- Encrypt media content stored in the system to prevent data theft during storage
- Use SSL/TLS and other encryption protocols during media content transmission to ensure data security in transit

## 3. Logging and Auditing
- Record critical system operations and access logs
- Enable auditing and tracing in the event of security incidents