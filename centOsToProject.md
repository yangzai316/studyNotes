## 基础前端项目部署-简记
这里主要针对基础的前端项目，不深入Linux的环境部署。这里可以启动node项目，vue、react...单页面项目。
### 服务器购买
这里使用阿里云,云服务器：CentOS 7.6 64位（自行购买）
### 域名购买
阿里云域名（自行购买）
### 域名备案
没有备案或是没有通过备案的网站，会被封锁，去阿里云的备案专区进行相关备案操作（如果你也是在阿里云购买的云服务），这里建议用阿里云APP进行备案，流程相对阶简单...
### 域名解析
到购买域名的网站进行解析，就是服务器IP指向的引导。
### 环境部署
上述步骤准备完毕，可链接自己的服务器进行部署。
阿里云提供链接自己服务器的页面，也可自己下载相关软件，如：Xshell... 
#### node安装
- 1、下载node
```
wget https://nodejs.org/dist/v10.15.0/node-v10.15.0-linux-x64.tar.xz
# 后面的链接地址是node的下载地址，可取node官网copy
# nod默认下载到你当前执行wget命令的位置，可先去你需要下载到的文件夹中在执行该命令
# 下载完成,会出现一个文件：node-v10.15.0-linux-x64.tar.xz
```
- 2、解压node
```
tar xJf node-v10.15.0-linux-x64 
# 解压完成，会出现一个node-v10.15.0-linux-x64文件夹，就是node了
```
- 2、测试node是否下载ok
```
cd node-v10.15.0-linux-x64/bin
# 会有node、npm，说明已下载完成
# 测试：
./node -v
# 出现node版本，说明安装ok
```
- 3、设置全局
```
# 在node-v10.15.0-linux-x64/bin里面执行：
ln -s node /usr/local/bin/node
# 或是根路径：ln -s /usr/node-v10.15.0-linux-x64.tar.xz/bin/node /usr/local/bin/
ln -s npm /usr/local/bin/npm
```
- 4、测试全局
```
node -v
npm -v
```
#### nginx安装

- 1、依赖项和必要组件
```
# 依次执行命令
yum install -y make cmake gcc gcc-c++  

yum install -y pcre pcre-devel

yum install -y zlib zlib-devel

yum install -y openssl openssl-devel
```
- 2、下载安装nginx
```
wget http://nginx.org/download/nginx-1.14.2.tar.gz
# 后面的链接地址是nginx的下载地址，可取nginx官网copy
```
- 3、解压
```
tar zxvf nginx-1.12.2.tar.gz && cd nginx-1.14.2
```
- 4、编译配置
```
./configure && make && make install
# 执行完本命令将会在 /usr/local/nginx 生成相应的可执行文件、配置、默认站点等文件
```
- 5、设置全局
```
ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx
```
- 6、启动
```
# 启动
nginx
# 重载加载配置
nginx -s reload
```
- 7、测试
```
nginx -t
# 出现：test is successful,说明安装ok
# 第一行会出现配置文件的位置，可进入修改配置，重启nginx
```
#### 安装pm2
- 1、安装node进程维护依赖，pm2
```
# 全局安装pm2
npm install pm2 -g
```
- 2、全局地址指向
```
ln -s /usr/node-v10.15.0-linux-x64.tar.xz/bin/pm2 /usr/local/bin/
```
- 3、启动node项目
```
# 运行node的入口文件，即可
pm2 start app.js
# 查看日志
pm2 log
# 查看运行项目列表
pm2 ls
```
#### 安装git
- 1、下载
```
yum install git
```
- 2、测试
```
git --version
```
### 尾声
本文是自行参照网友提供方法，自行安装过程的简介   
侵权联系删除














