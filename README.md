# image_processing
模块定义了一个ImageProcessing类，用于从共享内存读取图像，处理之后写入至另一段共享内存
### usages of class ImageProcessing
1、Attributes
* cam_name: 字符串，摄像头名称，如'front','back','plate',或者以数字命名
* lan_num： 字符串，摄像头所在车道序号
* cam_file_name: 字符串，映射为共享内存的普通文件的绝对路径，摄像头采集的图像会传送至该文件
* processed_file_name: 字符串，映射为共享内存的普通文件的绝对路径，处理后的图像会写入该文件
* server_ip: 字符串，Redis服务器ip
* server_port: 字符串，Redis服务器端口
* undistort: 布尔值，指示摄像头是否有畸变
2、Methods
* run
    :Usage:
      从共享内存读取图像，处理图像，再将处理后的图像写入另一段共享内存。最后将原图像和处理后的图像发布至Redis服务器
3、Example
  image_processing = ImageProcessing('plate','0','/tmp/master2','/tmp/master2_processed',
                                   'localhost','6379','')
  image_processing.run()
### Cautions
1、默认图像尺寸为1080p
2、处理图像的.so文件绝对路径为/home/westwell/Documents/wellocean/src/preprocessing/Preprocessing.so
3、图像透视变换矩阵绝对路径为/home/westwell/Documents/wellocean/src/param/perspective/project/lane_num/cam_name下，命名为cam_name.npy，如/home/westwell/Desktop/wellocean/src/param/perspective/zimao/channel_0/plate/perspective.npy，还要注意的是cam_name可能以数字命名，也可能以'plate'、'front'等命名
4、配置从Redis服务器topic名称为'/WellOcean/config'
5、该类的一个实例只会处理一个摄像头的图像
###
![image](./tmp/1.jpg)

