# CTFd-JavaWeb-Template

## 介绍

一个Java动态靶机镜像构建模板，用于CTFd搭建构建动态靶机镜像，本篇以2021年东华杯ezgadget作为例子

项目地址：https://github.com/LxxxSec/CTFd-JavaWeb-Template

随缘更新~

## 演示

docker镜像：`lxxxin/dhctf_2021_web_ezgadget`

![image-20220426203237353](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262032425.png)

![image-20220426203433380](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262034431.png)

## 如何使用

### 镜像构建

首先将本项目clone下来

```
git clone https://github.com/LxxxSec/CTFd-JavaWeb-Template
```

进入Template目录

```
cd Template
```

目录如下：

![image-20220426203652680](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262036718.png)



其中`_files`文件夹内存放了三个文件

- `flag.sh`：设置动态flag的脚本
- `start.sh`：启动JavaWeb的脚本
- `flag`：flag文件

其中`src`文件夹内存放jar包

![image-20220426203846094](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262038139.png)

使用时，放入替换`src`目录中的jar包

然后修改`Dockerfile`文件中的jar包文件名，并且根据自己的Tomcat等Web服务器端口情况开放

![image-20220426205616483](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262056518.png)

同理，修改`_files`目录下的`start.sh`的jar包文件名

![image-20220426204022323](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262040360.png)

进入到`Template`目录，使用下方的命令构建镜像（最后的点号不要漏掉！）

```
docker build -t 你的昵称/镜像名称 .
```

构建完成后，建议本地启动验证一下，防止push到dockerhub后有错：

```
docker run -it -d -p 本地端口:JavaWeb端口 你的昵称/镜像名称
```

进入本地镜像：

```
docker exec -it 容器ID /bin/sh
```

首先在浏览器验证JavaWeb是否能够正常运行

![image-20220426204907904](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262049943.png)

然后进入容器执行`cat /flag`

![image-20220426204739989](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262047031.png)

如果返回为空即正常

因为CTFd动态靶机是通过传入环境变量`$FLAG`实现动态flag的效果，本地因为`$FLAG`为空，经过替换后自然为空

接下来把镜像push到docker hub即可

```
docker push 你的昵称/镜像名称
```

### CTFd部署

首先当然需要一个CTFd动态靶场平台，搭建流程可以参考这个链接：https://www.xiinnn.com/article/33b63ea2.html

然后进入后台创建题目

![image-20220426205037784](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262050838.png)

选择动态镜像

![image-20220426205127669](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262051703.png)

分数根据自己需求即可，主要是下面三样设置，一定要配置好，容器内部端口不可以错

![image-20220426205502672](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262055715.png)

搭建完成后，不出意外的话，就可以访问了！

![image-20220426205703978](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262057036.png)

可以进入自己的云服务器题目对应的容器，动态flag也就生成啦！

![image-20220426205744455](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262057491.png)

## TODO

- 对文件夹的权限没有控制好，这个到时候修改
- 争取支持更多的JavaWeb中间件

## 交流群

有什么问题可以在群里提问，大家一起帮忙解决啦~

![IMG_2639(20220426-191834)](https://lxxx-markdown.oss-cn-beijing.aliyuncs.com/pictures/202204262100898.JPG)
