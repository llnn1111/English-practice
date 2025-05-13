 HEAD
龙青蜓：1.使用deepseek帮忙润色。2.使用deepseek教我怎样运行项目。3.使用deep seek查询项目相关软件（ffmepf）的相关语句指令3.使用deepseek教我在vscode里写readme.md插入图片5.使用deep seek教我怎么修改Markdown文档格式 6.使用deepseek了解项目具体的功能


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
