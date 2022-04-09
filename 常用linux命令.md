# 防火墙相关

```shell
//查看防火墙状态
firewall-cmd --state
// 关闭防火墙
systemctl stop firewalld.service
//禁止防火墙卡机自启动
systemctl disable firewalld.service 
//启动防火墙
systemctl start firewalld
// 防火墙开启https服务
firewall-cmd --permanent --zone=public --add-service=https
// 防火墙开启http服务
firewall-cmd --permanent --zone=public --add-service=http
```

# nginx相关



# 使用nginx部署Vue项目

1.安装nginx以及相关依赖

```shell
yum -y install gcc
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum install -y openssl openssl-devel
// 下载nginx到当前目录
wget http://nginx.org/download/nginx-1.9.9.tar.gz
// 解压缩
tar -zxvf nginx-1.9.9.tar.gz
cd /usr/local/web/nginx-1.9.9/
./configure
make
make install
```

安装好后可以在xshell里面 通过curl ip命令来确定是否安装成功

如果出现404页面则安装成功

curl 192.168.44.137

![image-20220405163323440](E:\work\notebook\image-20220405163323440.png)

2.修改配置

```shell
server {
		//监听端口
        listen       80;
        server_name  dist;
        // 配置前端项目地址
        root         /www/dist;
        location / {
        	// 配置前端项目地址
            root   /www/dist;
            index  /index.html index.htm;
        }
// 配置完成后
cd /usr/local/nginx/sbin
./nginx             # 启动
./nginx -s stop   	#停止
./nginx -s quit    	#比较安全的退出
./nginx -s reload 	#刷新重启
```

3.打包Vue项目

```shell
npm run build 生成dist文件夹压缩上传到/www/目录下
unzip dist.zip解压缩生成dist文件夹
```

4.关闭防火墙

```shell
//查看防火墙状态
firewall-cmd --state
// 关闭防火墙
systemctl stop firewalld.service
```

5.下载花生壳，配置内网穿透

![image-20220405163141208](E:\work\notebook\image-20220405163141208.png)

6.访问成功

![image-20220405163203924](E:\work\notebook\image-20220405163203924.png)

