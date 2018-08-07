# KrGallery

Crop , Video, Photos, from Telegram  

一个集**拍照和选择图片,裁剪**,**录制视频和选择视频**的强大且流畅简洁的库。


KrGallery摘取于[Telegram](https://github.com/DrKLO/Telegram "https://github.com/DrKLO/Telegram"),基于[@TelegramGallery](https://github.com/TangXiaoLv/TelegramGallery)开发,快速，高效，低耗,轻量级,使用简单。

- [功能](#功能)
- [效果](#效果)
- [安装](#安装)
- [用途](#用途)
    - [选择图片](#选择图片)
    - [拍照](#拍照)
    - [获取图片](#获取图片)
    - [录制视频](#录制视频)
    - [选择视频](#选择视频)
    - [获取视频](#获取视频)
    - [注意](#注意)
    - [API](#API说明)
- [TODO](#TODO)   
- [作者](#作者)
- [感谢](#感谢)
- [更变日志]()

## 功能

* 快速，高效，低耗
* 简易的整合,轻量级
* 基本没有依赖于任何的三方库
* 集拍照,选择图片,裁剪,录制视频和选择视频为一体

----------

## 安装

 [![](https://jitpack.io/v/chengzichen/KrGallery.svg)](https://jitpack.io/#chengzichen/KrGallery) [ ![Download](https://api.bintray.com/packages/chengzichen/maven/gallerylib/images/download.svg) ](https://bintray.com/chengzichen/maven/gallerylib/_latestVersion)

- 方式一:

**Step 1.  在根目录的gradle文件中配置**


**Add it in your root build.gradle at the end of repositories:**


	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}


**step2 添加依赖:**

	dependencies {
	     compile 'com.github.chengzichen:KrGallery:v1.03'
	}



- 方式二:


**Step 1.  在根目录的gradle文件中配置**

		allprojects {
				repositories {
					...
					 jcenter()
				}
			}


**step2 添加依赖:**


	dependencies {
		      compile 'com.dhc.krgallery:gallerylib:1.0.3'
		}



----------


## 效果
![Image text](https://github.com/chengzichen/KrGallery/raw/master/gif/photos.gif)
![Image text](https://github.com/chengzichen/KrGallery/raw/master/gif/selectcrop.gif)
![Image text](https://github.com/chengzichen/KrGallery/raw/master/gif/photocrop.gif)
![Image text](https://github.com/chengzichen/KrGallery/raw/master/gif/video.gif)

## 用途

### 选择图片
	
- **单选**(type:GalleryConfig.SELECT_PHOTO)
	
	    GalleryHelper
	    .with(MainActivity.this)			//Activity or Fragment
	    .type(GalleryConfig.SELECT_PHOTO)   //选择类型
	    .requestCode(12)					//startResultActivity requestcode 自己定义
	    .singlePhoto()						//选择单张图片
	    .execute();


- **多选**(type:GalleryConfig.SELECT_PHOTO)

	    GalleryHelper
	    .with(MainActivity.this)			//Activity or Fragment
	    .type(GalleryConfig.SELECT_PHOTO)	//选择类型
	    .requestCode(12)					//startResultActivity requestcode 自己定义
	    .limitPickPhoto(9)					//图片选择张数
	    .execute();


- **需要裁剪图片**
	
 		String outputPath = StorageUtil.getWritePath(StorageUtil.get32UUID() + ".jpg", StorageType.TYPE_TEMP);//定义裁剪图片输出在sdcard的位置

        GalleryHelper
		.with(MainActivity.this)			//Activity or Fragment
		.type(GalleryConfig.SELECT_PHOTO)   //选择类型
		.requestCode(12)					//startResultActivity requestcode 自己定义
		.singlePhoto()						//选择单张图片
		.isNeedCropWithPath(outputPath)		//需要裁剪并输出图片的路径,没有传入时返回数据为byte[]
		.execute();	



### 拍照
		
- 拍照

		GalleryHelper
		.with(MainActivity.this)   			//Activity or Fragment
		.type(GalleryConfig.TAKE_PHOTO)		//选择类型,拍照
		.requestCode(12)					//startResultActivity requestcode 自己定义
		.execute();	
	
	
- 需要裁剪图片 

		 outputPath = StorageUtil.getWritePath(StorageUtil.get32UUID() + ".jpg", StorageType.TYPE_TEMP);
         GalleryHelper
		.with(MainActivity.this)			//Activity or Fragment
		.type(GalleryConfig.TAKE_PHOTO)		//选择类型
		.isNeedCropWithPath(outputPath)		//需要裁剪并输出图片的路径,没有传入时返回数据为byte[]
		.requestCode(12)					//startResultActivity requestcode 自己定义
		.execute();

	**onActivityResult**


### 获取图片




> **在Acitivity 或者Fragment 中onActivityResult 方法**	


 		String path = dataIntent.getStringExtra(GalleryActivity.PHOTOS);


> **注意  :  需要裁剪并输出图片的路径,没有传入时返回数据为byte[]**



		byte[] datas =dataIntent.getByteArrayExtra(GalleryActivity.DATA);

### 录制视频(可限制录制时间)


		 GalleryHelper
		.with(MainActivity.this)    	//Activity or Fragment
		.type(GalleryConfig.RECORD_VEDIO)//选择类型
		.requestCode(12)				//startResultActivity requestcode 自己定义
		.limitRecordTime(10)            //定义录制视频时间
		.limitRecordSize(10)            //定义录制视频时间
		.execute();
		
### 选择视频
		
		 GalleryHelper
		.with(MainActivity.this)	 	//Activity or Fragment	
		.type(GalleryConfig.SELECT_VEDIO)//Activity or Fragment	
		.requestCode(12)				//startResultActivity requestcode 自己定义
		.isSingleVedio()				//是否是单选视频
		.execute();


### 获取视频

> **在Acitivity 或者Fragment 中onActivityResult 方法**


  		String path = data.getStringExtra(GalleryActivity.VIDEO);

### 注意

- **需要裁剪并输出图片的路径,没有传入时返回数据为byte[]**
- **选取多张图片时裁剪只对第一张照片有效**
- **选着视频目前支持单个视频**


### API说明
	
- 类[GalleryHelper](KrGallery/gallery/src/main/java/com/dhc/gallery/GalleryHelper.java) 
	
		1. with()    										//Activity or Fragment
		2. type(int type)  
			1.  GalleryConfig.SELECT_PHOTO  				//选择图片
			2.  GalleryConfig.TAKE_PHOTO 					//拍照
			3.  GalleryConfig.RECORD_VEDIO					//录制视频
			4.  GalleryConfig.SELECT_VEDIO					//选择单个视频
			5.  GalleryConfig.TAKEPHOTO_RECORDVEDIO 		//拍照和录制视频
		3. requestCode(int code) 				 			//startResultActivity requestcode 自己定义
		4. isSingleVedio()    								//选择单个视频,必须调用方法
		5. isNeedCropWithPath() 							//进行裁剪图片  返回一个传入路径值
		6. isNeedCrop()										//需要裁剪图片 这将返回一个  byte[] data数据类型
		7. selectVedioWithMimeTypes()						//filter of media type， based on MimeType standards：{http://www.w3school.com.cn/media/media_mimeref.asp}<Li>eg:new string[]{"image/gif","image/jpeg"}
		8. hintOfPick()										//hint of Toast when limit is reached
		9. singlePhoto()									//选择单张照片
		10. limitPickPhoto(int)  							//hint of Toast when limit is reached
		11. limitRecordTime(int)                            //限制视频录制的时间
		11. execute()


## TODO

- 修改部分样式 
- 自定义主题
- 视频的编辑
- 图片的编辑
- 提供压缩
- 优化代码


## 作者



-  github: [@chengzichen](https://github.com/chengzichen)


-  博客 : [邓浩宸的博客](https://chengzichen.github.io/)


## 感谢 



> [@Telegram](https://github.com/DrKLO/Telegram "https://github.com/DrKLO/Telegram")



> [@TelegramGallery](https://github.com/TangXiaoLv/TelegramGallery)

## 友情链接



> [@XDroid](https://github.com/limedroid) 老司机