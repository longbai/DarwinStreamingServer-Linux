#!/bin/bash
groupadd qtss
adduser -s /sbin/nologin qtss -g qtss

wget http://static.macosforge.org/dss/downloads/DarwinStreamingSrvr6.0.3-Source.tar
tar -xvf DarwinStreamingSrvr6.0.3-Source.tar

mv DarwinStreamingSrvr6.0.3-Source DarwinStreamingSrvr6.0.3-Source.orig

wget http://parsa.epfl.ch/cloudsuite/software/darwin/dss-6.0.3.patch
patch -p0 < dss-6.0.3.patch

mv DarwinStreamingSrvr6.0.3-Source.orig DarwinStreamingSrvr6.0.3-Source

wget http://parsa.epfl.ch/cloudsuite/software/darwin/dss-hh-20080728-1.patch
patch -p0 < dss-hh-20080728-1.patch

cd DarwinStreamingSrvr6.0.3-Source

mv Install Install.orig
wget http://parsa.epfl.ch/cloudsuite/software/darwin/Install
chmod +x Install

./Buildit
./Install
---End Instal Script-------------------------------

1. 安装完毕后，你可以看到启动进程：
ps ax |grep Darwin

2. 启动管理控制面板页面
/usr/bin/perl /usr/local/sbin/streamingadminserver.pl

3. 通过1220端口可以访问web管理页面:

http://IP:1220/

4. 用安装过程中设置的管理账户和密码登录，进入设置向导，可以不输入直接点击[Next]按钮
注意媒体文件的路径，你以后会用到，是存储音视频媒体文件的根目录

5. 在web管理页面中打开Playlists子页面，进行播放列表管理。
增加1个媒体文件的步骤:
a. 先通过ftp，sftp，ssh上传到第4步中所在的目录下
b. 在web管理页面的Playlists中新建一个播放列表
c. 把媒体目录下的文件（左侧列表）双击，移动到右侧播放列表中
d. 保存即可
e. 然后选中播放列表，点击start

6.上传的mp4,3gpp等文件需要被hint后才能播放，否则第5步会报错
具体参考：
http://www.videohelp.com/tools/mp4box这里下载到了mp4box，在dos命令行操作
下载到到解压出后会有个叫 mp4box.exe ，用它在命令行下面运行
mp4box test.mp4 -hint

7.用vlc播放器测试刚才添加的媒体,打开网络流，输入rtsp URL测试

来源 http://www.mworkbox.com/wp/work/223.html
