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