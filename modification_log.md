 HEAD
 HEAD
 <!--by 龙青蜓-->
龙青蜓：1.使用deepseek帮忙润色。2.使用deepseek教我怎样运行项目。3.使用deep seek查询项目相关软件（ffmepeg）的相关语句指令3.使用deepseek教我在vscode里写readme.md插入图片5.使用deep seek教我怎么修改Markdown文档格式 6.使用deepseek了解项目具体的功能


龙青蜓：1.使用deepseek帮忙润色。2.使用deepseek教我怎样运行项目。3.使用deep seek查询项目相关软件（ffmepf）的相关语句指令3.使用deepseek教我在vscode里写readme.md插入图片5.使用deep seek教我怎么修改Markdown文档格式 6.使用deepseek了解项目具体的功能
52b8fd528e475fdb80b44439682da8d7008fbfba


<!-- by 韦柔 -->
## 1. 搜索格式
查找常用到的标准的Markdown文档格式，标题、文字样式、表格、行内代码等等应该用什么格式。
 
如将视频编码里面“1.2 User Configuration: The system manages video encoding through preset configuration files and API interfaces. Users can configure parameters including codec (e.g., libx264), profile (e.g.,high422/main), bitrate, framerate, and resolution through the interface.”改写为：
 
### 1.2 User Configuration
The system manages video encoding through preset configuration files and API interfaces. Users can configure parameters including:
- Codec (e.g., libx264)
- Profile (e.g., high422/main)
- Bitrate
- Framerate
- Resolution
 
## 2. 前期准备
了解自己所负责说明功能的参数，通过AI询问运行截图里面的一些陌生参数，让AI详细解释一下这些关键参数，以助于进一步说明视频编码的功能，音频编码、图片编码也是如此。
 
### 如视频编码的通用参数的解释
- **Profile Key**：预设的唯一标识ID（如18、29等）。
- **Label**：预设的名称，通常包含编码格式、分辨率等关键信息（如MMS_MP4_H264_6000kb_veryslow_720p50_high422_AAC_160）。
- **Content Type**：固定为Video，表示这些预设用于视频编码。
- **File Format**：输出视频的封装格式（如mp4、dash、ts）。
 
## 3. 术语审核
用AI进行英文的语法和专业术语检查，并将有错误的英文进行输出。
 
- 如在通信功能的英文版中将"realizes"改为更符合场景的"facilitates"（"实现"→"促成"）。
- 补充冠词"the"使"system support team"更规范。
- 统一使用"email"替代"mail"（更符合现代技术术语）。
 
## 4. 预测功能
用AI预测该媒体管理系统的所需要到的安全功能，并查看该系统是否有这样安全功能，如有符合的，可加入到安全功能说明里面。
 
### 如
- **身份认证**：需要通过电子邮箱、密码等方式验证用户身份。
- **数据加密**：对系统中存储的媒体内容进行加密。
 
这些该系统都存在，可进一步添加到里面。
<!-- by 韦柔 -->


<!-- by 梁梅 -->
项目初期接手时，面对庞大的代码库我确实有些无从下手，没有思路也没有头绪，我就将项目的主要文件截图给Deepseek,让它帮我分析哪些文件是完成主要功能教程任务的重点文件。通过它的分析，我得知MMSEngine/src 、 MMSEngineService/src和docs是完成这个任务的关键。接下来我根据这几个文件去寻找项目中的主要功能，主要有以下功能：
1. 内容摄入功能 2.内容处理功能 3.内容编码功能 4. 通知功能 5. 特效处理功能 6.视频速度调整功能 7.人脸识别与识别功能 8.直播处理功能 9.其他功能
我主要负责的是第7第8点。我将EncoderProxy.cpp文件里面的代码喂给它，我让它帮我分析出了CatraMMS 人脸识别功能、人脸身份识别功能、直播网格功能、直播录制功能的使用教程，其中还会给出一些看得懂的例子，例如
场景：一场线上会议，需要把主讲人镜头、PPT共享、观众互动三个画面拼成一个网格直播。
操作流程：注册三个直播流 → 分别起名 主讲人、PPT、观众。
写任务单子：
    分3列，总分辨率1920x1080（每个小画面640x1080）。
    输出地址填公司的直播推流地址。
    提交任务 → 系统自动合成画面并推流。
    观众看到三列画面同步播放，效果像专业直播！
在编写技术文档时遇到个小插曲——不熟悉VS Code的图片插入操作，后来通过即时咨询Deepseek解决了这个问题。其次，我还让它帮我将我所写的内容加工一下，使其看起来专业一点。


<!--by 罗娜-->

1. 我从项目中找到专业术语后，发给ai，让他帮我进行分类

2. 找到项目关系图后，让ai用简单的框架帮我将项目关系简洁化

3. 术语分类完成后，内容不整齐，我让ai使用Markdown形式帮我优化术语表

<!--by 罗娜-->

<!--by 韦淑静-->

AI使用说明：

1、前期准备：使用什么工具、如何使用工具完成本次作业。
我向AI提问运行该项目需要准备哪些工具，以及如何正确的使用工具。例如，如何Fork他人的仓库，怎么写README.md等文件。

2、对项目入手：
首先向AI提问如何对项目入手，充分了解我们选择的开源项目是什么东西，了解到这个项目是开发了一个媒体管理系统平台。其次是专研这个系统是如何构造的，以及具备了哪些功能。了解各个功能的作用以及他们的实现逻辑，最后我们研究这个系统的各个功能如何使用，牢记其使用的步骤，使用这个系统执行任务后得到什么样的作品。

3、编辑好文本（中文版）之后让AI润色，让AI检查句子是否包含病句，术语是否专业，逻辑是否清晰。

生成对比（截取部分）：

（1）图片叠加到视频上（AI前）

实现方式：在工作流配置里通过定义任务来完成此操作。配置中使用了 GroupOfTasks 类型，其中包含Add - Content子任务，该子任务是添加视频源，在后续步骤中会有对overlay特效的配置。在项目中，会使用视频处理库（如 FFmpeg），通过在配置文件中设置overlay相关参数，将图片叠加到视频上。

作用
此功能可用于视频编辑、广告制作、影视后期等领域。例如在广告视频中，可以将品牌 logo 叠加到视频画面上；在影视后期制作中，可添加特效图片营造特定氛围。

使用教程
准备素材：准备好要叠加的图片和视频文件。
创建工作流配置文件：定义任务类型和参数。
执行工作流：将配置文件提交给系统，系统会根据配置完成图片叠加到视频上的操作。

（1）图片叠加至视频（AI后）

实现逻辑：通过工作流配置文件定义任务链实现。在配置文件中采用GroupOfTasks类型，嵌套Add-Content子任务加载视频源，并通过FFmpeg等专业视频处理库配置overlay参数，完成图片的精准叠加。

应用场景：广泛应用于广告制作（如嵌入品牌logo）和影视后期（如添加特效氛围图层）等领域。

操作步骤：
素材准备：整理待叠加图片与目标视频文件。
配置文件编写：定义任务类型及参数（如叠加位置、透明度等）。
任务执行：提交配置文件，系统自动完成特效合成。

4、编写英文版后喂给AI润色，让AI检查我书写的英文内容是否有语法错误、词汇搭配不当，专业术语是否使用得当，并对其进行修改，让内容更加专业流畅。

生成对比（截取部分）：
Special Effects Processing Function（AI前）

(1) Picture Overlay on Video Implementation Logic: Achieved by defining a task chain in the workflow configuration file. Use the GroupOfTasks type in the file, nest the Add-Content subtask to load the video source, and configure overlay parameters via FFmpeg or other professional video processing libraries for precise picture overlay. Application Scenarios: Widely used in advertising production (e.g., embedding brand logos) and film post-production (e.g., adding atmospheric effect layers). Operational Steps:
Material Preparation: Organize pictures to be overlaid and target video files.
Configuration File Writing: Define task types and parameters (e.g., overlay position, transparency).
Task Execution: Submit the configuration file for automatic effect synthesis by the system.
Operation is as shown below: Prepare the video file and pictures to be overlaid, and select the workflow editor on the page (as shown below).
In the workflow, add the required subtasks. The functions can be seen in the left task library panel (as shown below). Add the subtask for picture overlay on video, define the task type and parameters, and save the properties.

Special Effects Processing Function（AI后）

(1) Picture Overlay on Video Implementation Logic: This is implemented by defining a task chain in the workflow configuration file. In the file, specify the GroupOfTasks type and nest the Add-Content subtask to load the video source. Then employ FFmpeg or other professional video processing libraries to configure overlay parameters, enabling precise picture overlay.
Application Scenarios: It is widely used in advertising production (e.g., embedding brand logos) and film post - production (e.g., adding atmospheric effect layers).
Operational Steps:
Material Preparation: Prepare the pictures to be overlaid and the target video files.
Configuration File Writing: Define task types and parameters (e.g., overlay position, transparency, etc.).
Task Execution: Submit the configuration file and the system will automatically synthesize the effects.
The operation is as shown below: Prepare the video file and the pictures to be overlaid. Select the workflow editor on the interface (refer to the following illustration).

5、编辑README.md等文件时，遇到不知道如何插入截图问题，向AI提问。

6、编辑README.md等文件后，向AI提问如何把编辑好的内容提交并上传到远程仓库。

7、向AI提问如何创建文件夹并推送到仓库。

<!--by 韦淑静-->

 a13547a4ed8381c35d6f1344acddbf5076f1406a

