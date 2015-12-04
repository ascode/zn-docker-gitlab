# zn-docker-gitlab
这个文章尽量记录一些我使用gitlab-ce的官方镜像遇到的问题和心得

### 设置groups的Group path
group path这个参数经过测试，发现是http请求转发链路中的最后一个请求的url，也就是说，如果你用了nginx做反向代理,那么最后一个直接条转到服务的地址就决定了gitlab里面显示的地址

### gitlab上传大文件的问题
刚开始,我使用http方式，结果一遇到文件有个800kb或者文件数量有30个，就开始报错：  
error: RPC failed; result=22, HTTP code = 413  
#### 排除百度的干扰
百度上搜索，一搜一大堆，看了都不能解决问题。  
百度方法如下：  
1. 增加gitlab object的最大大小  
2. 增加nginx的允许的最大client_body的大小  
。。。  
网上找了很多方法，不一一列举，试了都没用。我总结的方法就是使用ssh连接。只是这里使用ssh地址书写方式有讲究，具体如下：  

#### 使用ssh
命令git clone ssh://git@***.***.cn:100**/enjiafuture/nidexiangmumingcheng.git  

这里不得不提一下，gitlab装好后，建立项目之后，项目中提示的命令是这样的：  
git clone git@c270a50be95a:enjiafuture/ef-web.git  
这个官方推荐的命令根本行不通   


我把官方的贴在下面  
<pre style="font-size:12px;font-color:gray;">
The repository for this project is empty  

If you already have files you can push them using command line instructions below.  
Otherwise you can start with adding README file to this project.  

Command line instructions


Git global setup

git config --global user.name "jinfei"  
git config --global user.email "ascode@icloud.com"  

Create a new repository

git clone git@c270a50be95a:enjiafuture/ef-web.git  
cd ef-web  
touch README.md  
git add README.md  
git commit -m "add README"  
git push -u origin master  

Existing folder or Git repository  

cd existing_folder  
git init  
git remote add origin git@c270a50be95a:enjiafuture/ef-web.git  
git add .  
git commit  
git push -u origin master  
</pre>



