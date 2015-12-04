# zn-docker-gitlab
这个文章尽量记录一些我使用gitlab-ce的官方镜像遇到的问题和心得

### 设置groups的Group path
group path这个参数经过测试，发现是http请求转发链路中的最后一个请求的url，也就是说，如果你用了nginx做反向代理,那么最后一个直接条转到服务的地址就决定了gitlab里面显示的地址
