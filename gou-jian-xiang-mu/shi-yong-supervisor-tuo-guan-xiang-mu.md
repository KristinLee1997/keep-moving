# 使用supervisor托管项目

## 安装

{% embed url="https://love-coding.gitbook.io/learning/linux/supervisor/an-zhuang-supervisor" %}

## 使用

1.更改supervisord.conf，添加想要运行项目的信息

注意：配置中的路径尽量要写绝对路径啊。。。

![](../.gitbook/assets/image%20%2813%29.png)

2.执行以下命令

```text
supervisorctl -c supervisord配置文件路径
```

进入supervisor客户端后执行reload\(重启supervisor，重新加载配置文件\) 

执行status查看项目是否运行，显示RUNNING就是正常运行啦

![](../.gitbook/assets/image%20%283%29.png)













