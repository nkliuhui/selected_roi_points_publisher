# 简介:  
* 这是一个RVIZ插件, 用于在RVIZ中选取感兴趣区域的点云数据并自动发布一帧sensor_msgs::PointCloud2消息.  
* 待编译完成之后, 可以在RVIZ中找到这一插件工具  
# 使用:  
可参考readme.txt
# Note:  
这一工具来自 https://github.com/Anto09/selected_points_publisher.git  
* 重写了CMakeLists.txt文件, Ubuntu 16.04和18.04编译无误.  
* 由于"选取规则(貌似是依据法向量判断了一下)"问题, 大部分点可以被选中, 小部分被忽略了...