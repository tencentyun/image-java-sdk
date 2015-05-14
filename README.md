qcloud-java-sdk
===================================
简介
----------------------------------- 
java sdk for picture service of tencentyun.

版本信息
----------------------------------- 
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

### 2. 创建PicCloud对象
		
	PicCloud pc = new PicCloud(APP_ID, SECRET_ID, SECRET_KEY);

### 3. 调用对应的方法
上传
		
	UploadResult result = new UploadResult();
	int ret = pc.Upload(userid, pic, result);
	if(ret == 0){
		System.out.println("upload pic success");
		result.Print();
	}else{
		System.out.println("upload pic error, error code="+ret);
	}
复制
		
	UploadResult result = new UploadResult();
	int ret = pc.Copy(userid, fileid, result);
        if(ret == 0){
        	System.out.println("copy pic success");
        	result.Print();
        }else{
        	System.out.println("copy pic error, error="+pc.GetError());
	}
查询
		
	PicInfo info = new PicInfo();	
	int ret = pc.Stat(userid, fileid, info);
	if(ret == 0){
        	System.out.println("Stat pic success");
        	info.Print();
        }else{
        	System.out.println("Stat pic error, error="+pc.GetError());
	}
删除
	ret = pc.Delete(userid, fileid);
        if(ret == 0){
        	System.out.println("delete pic success");
        }else{
        	System.out.println("delete pic error, error="+pc.GetError());
	}
下载
		
	//根据是否开启防盗链，选择正确的下载方法
	//不开启防盗链
	//ret = pc.Download(userid, result.fileid, "./download.jpg");
	//ret = pc.Download(result.download_url, "./download.jpg");
	//开启防盗链
        ret = pc.DownloadEx(userid, result.fileid, "./download.jpg");
        if(ret == 0){
        	System.out.println("download pic success");
	}else{
        	System.out.println("download pic error, error="+pc.GetError());
	}	
	
