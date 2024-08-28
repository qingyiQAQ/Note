购买服务器

安装java

安装MCSmanager

apt update && apt install wget && apt install git

sudo wget -qO- https://gitee.com/mcsmanager/script/raw/master/setup_cn.sh | bash

设置MCSM为开机自启

systemctl enable mcsm-{daemon,web}.service

上传forge文件，启动命令如下

java -server -Dfile.encoding=UTF-8 -Duser.language=zh -Duser.country=CN -jar ${ProgramName} --installServer

修改run.sh

-server -Dfile.encoding=UTF-8 -Duser.language=zh -Duser.country=CN

![image-20240103182033698](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20240103182033698.png)

启动命令设置为bash run.sh

启动