qcloud-java-sdk
===================================
简介
----------------------------------- 
java sdk for picture service of tencentyun.

版本信息
----------------------------------- 
### v2.0.0
支持2.0版本的图片restful api。内部实现了高度封装，对开发者透明。

### v1.2.1
增加视频分片上传功能，较大视频可使用分片上传。

### v1.2.0
稳定版本，支持微视频的基本api。
包括视频的上传、下载、查询和删除。

### v1.0.0
稳定版本，支持图片云的基本api。
包括图片的上传、下载、复制、查询和删除。

### v0.0.1
初始非稳定版本，仅支持上传。后续将会继续完善。

How to start
----------------------------------- 
### 1. 在[腾讯云](http://app.qcloud.com) 申请业务的授权
授权包括：
		
	APP_ID 
	SECRET_ID
	SECRET_KEY
2.0版本的云服务在使用前，还需要先创建空间。在使用2.0 api时，需要使用空间名（Bucket）。

### 2. 创建对应操作类的对象
如果要使用图片，需要创建图片操作类对象
		
	v1版本	
	PicCloud pc = new PicCloud(APP_ID, SECRET_ID, SECRET_KEY);
		
	v2版本
	PicCloud pc = new PicCloud(APP_ID, SECRET_ID, SECRET_KEY, Bucket);
	
如果要使用视频，需要创建视频操作类对象
		
	VideoCloud vc = new VideoCloud(APP_ID, SECRET_ID, SECRET_KEY);	

### 3. 调用对应的方法
上传
		
	UploadResult result = new UploadResult();
	int ret = pc.Upload(userid, pic, result);
	ret = vc.Upload(userid, video,"test_title","test_Desc","test_magic_context", result);
	//视频分片上传
	ret = vc.SliceUpload(userid, video,"test_title","test_Desc","test_magic_context", result);
复制
		
	UploadResult result = new UploadResult();
	int ret = pc.Copy(userid, fileid, result);
查询
		
	PicInfo picInfo = new PicInfo();	
	int ret = pc.Stat(userid, fileid, picInfo);
	VideoInfo videoInfo = new VideoInfo();	
	ret = vc.Stat(userid, fileid, videoInfo);
删除
		
	ret = pc.Delete(userid, fileid);
	ret = vc.Delete(userid, fileid);
下载
		
	//根据是否开启防盗链，选择正确的下载方法
	//不开启防盗链
	//ret = pc.Download(userid, result.fileid, "./download.jpg");
	//or
	//ret = pc.Download(result.download_url, "./download.jpg");
	//开启防盗链
    ret = pc.DownloadEx(userid, result.fileid, "./download.jpg");
	ret = vc.DownloadEx(userid, result.fileid, "./download.mp4");
