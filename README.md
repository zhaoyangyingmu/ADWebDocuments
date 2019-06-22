# ADWeb小程序项目文档汇总

这个小程序用于实现一个[互动教学](https://github.com/2019-web/project_mini_edu)的项目。

## 项目成员
[谢东方](https://github.com/zhaoyangyingmu)，[张健](https://github.com/DarkYoung)，[陈雷远](https://github.com/radarcly)，[陈涛](https://github.com/ChenTao98)

## 项目分工
* 谢东方
    - 小程序： 笔记和收藏查看、添加的页面，以及和后端相关api的对接。
    - 小程序后端：参与设计数据库，笔记和收藏api，获取OpenID的api的书写，以及相关文档的书写。
    - 教师端后台：登陆和注册页面以及相关流程，利用spring security机制进行保护，教师信息维护界面。
    - 部署： 相关全部工作。
* 张健

* 陈涛
    - 协助设计数据库
    - 教师端开发
        * 负责生成数据库操作接口（包括小程序后端项目的有关接口）
        * 完成教师课程页面的所有功能
        * 完成查看学生信息页面所有功能
    - 协助测试微信小程序
    - 协助修改小程序后端的bug
* 陈雷远 
    - 小程序后端开发：
        * 数据库表设计与构造
        * 用户相关api
            + 获取学生信息
            + 修改学生信息
            + 判断用户是否已注册
        * 课程相关api
            + 选课，获取课程分类，获取课程列表，获取主题列表，获取分类课程，获取主题课程列表，获取学生选课列表，获取课程详细信息
            + 获取小节知识点，获取小节测试，提交测试
        * 协助前端完成微信小程序功能测试，编写微信小程序项目文档。



## 项目相关文档地址

* [小程序](https://github.com/DarkYoung/ADCourse)
    - 项目地址： https://github.com/DarkYoung/ADCourse
    - 说明文档地址： https://github.com/DarkYoung/ADCourse/blob/master/README.md
    - 用户手册地址： https://github.com/DarkYoung/ADCourse/blob/master/%E7%94%A8%E6%88%B7%E6%89%8B%E5%86%8C.md

* [小程序后端](https://github.com/ChenTao98/adWebApi)
    - 项目地址：https://github.com/ChenTao98/adWebApi
    - 说明文档地址：https://github.com/ChenTao98/adWebApi/blob/master/README.md
    - api接口说明地址（密码：123456）：https://www.showdoc.cc/379113643189792?page_id=2197030605969803

* [教师端](https://github.com/ChenTao98/adWebBack)
    - 项目地址： https://github.com/ChenTao98/adWebBack
    - 说明文档地址：https://github.com/ChenTao98/adWebBack/blob/master/README.md
    - 用户手册地址：https://github.com/ChenTao98/adWebBack/blob/master/%E6%95%99%E5%B8%88%E7%AB%AF%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E.md

## 项目部署
* 小程序后端访问地址： http://47.102.201.65:18081
* 教师端访问地址： http://47.102.201.65:18080 
* 部署文件目录： https://github.com/ChenTao98/adWebBack/tree/master/docker
* 部署过程：
    - 通过windows端batch脚本上传文件到服务器
    - 在服务器端运行脚本程序，脚本程序完成以下内容：
        * 通过Dockerfile创建自定义镜像
        * 关闭原有的docker容器
        * 通过docker-compose命令，开启互连的容器（通过自定义的docker network互连，桥接网络）
            - docker-compose中挂载当前的db目录，和static目录。前者用于数据库文件持久化，后者用来存储图片和tomcat的输出日志。
            - 建立18080和18081端口的映射。
    - 通过docker cp ./adweb_project.sql container_name:/root命令将文件复制到容器中。通过docker exec -it container_name /bin/bash进入容器，source /root/adweb_project.sql，创建数据库与表格。如果不是第一次部署，这一步可以忽略，因为之前的数据已经被持久化到db目录下。

