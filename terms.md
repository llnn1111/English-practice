术语	                       英文	                              说明

1. 系统架构组件

       
多媒体服务引擎数据库门面	  mmsEngineDBFacade	                 数据库访问抽象层
内容分发授权管理器         	 MMSDeliveryAuthorization	         内容发布权限控制
编码器负载均衡器	         EncodersLoadBalancer	             编码资源动态分配


2. 任务调度与管理

      
任务组容器                    GroupOfTasks	                   批量任务聚合单元
并行执行模式	              executionType: "parallel"	       任务并发策略
任务队列优先级	              encodingPriority: "High"	       处理优先级控制
定时任务周期	              ulPeriodInMilliSecs	           周期任务时间间隔


3. 视频/图像处理

    
人脸检测模型	             cascadeName	                     OpenCV特征分类器
初始帧跳过数	             initialFramesNumberToBeSkipped	     视频处理起始偏移
任务执行起始时间	         processingStartingFrom	             计划任务触发时间


4. 资源与队列

     
低优先级编码队列         	lowPriorityEncodingJobs	              后台任务存储池
人脸识别计数器          	faceRecognitionNumber	              并发任务统计


5. 存储与生命周期

     
内容过期天数	             expirationInDays	                 自动清理时间阈值
文件系统访问开关	         noFileSystemAccess	                 安全访问控制


6. 网络与IO控制

  
FastCGI互斥锁	             fcgiAcceptMutex	                请求接收同步控制
文件上传跟踪器	             FileUploadProgressData	             传输状态监控


7. 线程安全机制


定时任务互斥锁	              _mtTimesMutex	                    周期任务线程保护



<!--by 罗娜-->
