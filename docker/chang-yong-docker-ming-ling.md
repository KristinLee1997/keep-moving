# 常用docker命令

重启Mysql： docker restart mysql5

Mysql5.7启动客户端： docker exec -it mysql5 /usr/bin/mysql -u root -p  


Redis启动：docker run -it --rm redis:5.0.4 redis-cli -h 机器ip

                      docker exec -it 214225791aa3 redis-cli

                      docker exec -it redis redis-cli

启动Zookeeper：

                       docker exec -it 容器id zkCli.sh



