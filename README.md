# fastDFS
fastdfs和Springboot集成纯demo，无其它集成

fastdfs单机部署+nginx步骤：
需要用到的工具：
1.fastdfs-6.06.tar.gz
2.fastdfs-nginx-module-1.22.tar.gz
3.libfastcommon-1.0.43.tar.gz
4.nginx-1.16.1.tar.gz
将上述文件拷贝到linux上

安装 & 配置 FastDFS
1.  tar -xvf fastdfs-5.05.tar.gz
2.  cd fastdfs-5.05/
3.  ./make.sh && ./make.sh install

注意：FastDFS 默认安装方式安装后启动路径为
/etc/init.d/fdfs_storaged 
/etc/init.d/fdfs_trackerd 

FastDFS 服务脚本设置的 bin 目录是 /usr/local/bin， 但实际命令安装在 /usr/bin/
#创建软链接
ln -s /usr/bin/fdfs_trackerd   /usr/local/bin
ln -s /usr/bin/fdfs_storaged   /usr/local/bin
ln -s /usr/bin/stop.sh         /usr/local/bin
ln -s /usr/bin/restart.sh      /usr/local/bin

配置 FastDFS tracker
1.  cp tracker.conf.sample tracker.conf
2.  mkdir -p fastdfs/tracker_data
3.  vim /etc/fdfs/tracker.conf
可能需要修改的配置：
  # 配置文件是否不生效，false 为生效
  disabled=false
  #后面为绑定的IP地址 (常用于服务器有多个IP但只希望一个IP提供服务)。如果不填则表示所有的  我自己demo写的本机ip（非内网IP）
  bind_addr=xxx.xxx.xxx.xx
  # 提供服务的端口（随意你）
  port=22122
  # Tracker 数据和日志目录地址(根目录必须存在,子目录会自动创建，如果没有创建就自己创建)
  base_path=/home/xxxx/fastdfs/tracker_data
  # HTTP 服务端口
  http.server_port=80
  
启动tracker：/etc/init.d/fdfs_trackerd start
监听端口 22122 (Tracker服务安装成功)：netstat -nvlpt|grep fdfs



  
  
  
  
