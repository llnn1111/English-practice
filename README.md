<!-- by 韦柔 -->
Content encoding function
![Screenshot 1 of video coding function](images/Encoding%20function.png)
1.	Video encoding:
The content encoding function of catramms provides flexible video encoding configuration options and supports multiple formats and parameter settings.
The system realizes video coding management through preset configuration files and API interfaces. Users can configure codec (such as libx264), profile (such as high422/main), bit rate, frame rate, resolution and other parameters in detail in the interface.
The core function code is located in API/src/API_Encoding.cpp, which contains key functions such as addEncodingProfile(), removeEncodingProfile(), and is used to add and delete encoding configurations.
![Screenshot 1 of video coding function](images/Video%20encoding1.png)
Predefined video coding schemes are stored in the predefined encoding predefinedEncodingProfiles/video directory and managed in JSON format.
As can be seen from the figure, the system supports MP4, DASH, TS and other container formats, and provides preset options for a variety of bit rate and resolution combinations, which are suitable for video coding requirements of different scenes.
![Screenshot 2 of video coding function](images/Video%20encoding2.png)

2.	Audio encoding:
The audio coding function can be used as an independent module, or it can work together with video coding.
From the audio parameters in the video coding configuration (such as AAC_160), it can be seen that the system uses AAC as the core audio coding format and provides multiple bit rates from 92kbps to 160kbps.
Predefined audio coding schemes are stored in the predefined encoding predefinedEncodingProfiles/audio directory and managed in JSON format.
Professional audio processing will include loudness normalization, noise suppression and intelligent segmented coding technology, which is especially suitable for podcasting and music applications.
The support of multi-channel audio shows that the system can handle professional audio formats such as 5.1 surround sound and meet the requirements of high-quality media production.
![Screenshot of audio coding function](images/Audio%20encoding.png)

3. Image encoding:
This function supports mainstream format conversion and intelligent compression.
The system provides a preset template of "MMS_JPEG_85Q_1920x1080", including quality parameters (85Q) and resolution options.
These predefined image coding schemes are stored in the predefined encoding predefinedEncodingProfiles/image directory and are structured in JSON format.
Progressive loading and adaptive format selection will be particularly optimized for web applications, and the mobile terminal may provide the function of automatically generating multiple resolution versions that adapt to different screen sizes.
The image processing engine should support metadata retention, automatic direction correction and other professional features, and can batch process a large number of image files, significantly improving the efficiency of content management.
![Screenshot of audio coding function](images/Image%20encoding.png)
