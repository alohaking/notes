### 开发服务器

```shell
# 登录开发mysql
sudo su - jenkins
# 密码  testAbc123
docker exec -it coloredgedb mysql -uroot -p
```

```
1）在jenkins里面点击“立即构建”
2）jenkins的任务完成以后，登录到build这台机器，把服务关闭 sudo service cp-server stop
3）查看是否有appserver 的java进程还在 ， ps aux | grep java 命令可以看的
4）如果有的话，就kill -9 把它干掉
5）切换到workspace（/var/lib/jenkins/workspace/coloredge-develop）目录，sudo nohup ./mvnw & 这个命令去启动
6)  浏览器检查启动结果
```

### 地址

```
https://ce-cp-test.phyworks.cn/ # 测试
http://ce-cp.phyworks.cn/ # 开发
http://ce-cp-api.phyworks.cn/ # 开发api
```

### jira

```
https://ny.avantifytech.com/
```



### SSH

```shell
# 开发环境
ssh zhanghx@build.phyworks.cn
# 测试环境
ssh zhanghx@118.190.65.117
#QA
ssh ec2-user@collaboration-qa.coloredge.com
# python脚本
ssh ec2-user@18.212.20.227
# CE生产环境
ssh ec2-user@collaboration.coloredge.com
```

### Jenkins

``` shell
# http://build.phyworks.cn
# hengxian / qGGs55LNKYcx
```

### git

```shell
ssh://git@ny.avantifytech.com/coloredge/collaboration/appserver
ssh://git@ny.avantifytech.com/coloredge/collaboration/web

# als
ssh://git@ny.insigmaus.com/als/pricentric/appserver
```

### 墨刀

```
https://org.modao.cc/app/b064fa97e78214f36bb505007c067bbbbaab8963#screen=s4761b401d2155600523300
```



```sql
  INSERT INTO `jhi_user` (`id`, `login`, `password_hash`, `first_name`, `last_name`, `email`, `image_url`, `activated`, `lang_key`, `activation_key`, `reset_key`, `created_by`, `created_date`, `reset_date`, `last_modified_by`, `last_modified_date`, `status`, `password_change_date`) VALUES (14, 'testuser', '$2a$10$VEjxo0jq2YG9Rbk2HmX9S.k1uZBGYUHdUcid3g/vfiEl7lwWgOH/K', 'Test', 'AE', 'ting.yao@phyworks.cn', 'https://ce-philip-dev.s3.us-west-1.amazonaws.com/avatar/ting14?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20190617T141304Z&X-Amz-SignedHeaders=host&X-Amz-Expires=432000&X-Amz-Credential=AKIAY2WCGSDAZ7FJNHYJ%2F20190617%2Fus-west-1%2Fs3%2Faws4_request&X-Amz-Signature=52fadf3a3155a76d1bd75bba28537c5984beb0ee73cea9867e25c257e998c69e', 1, 'en', NULL, NULL, 'admin', '2019-06-17 14:22:04', NULL, 'admin', '2019-06-17 14:22:04', 'ACTIVE', '2019-06-17 14:12:51');
```

```mysql
select
  TABLE_NAME,COLUMN_NAME,CONSTRAINT_NAME
from INFORMATION_SCHEMA.KEY_COLUMN_USAGE
where CONSTRAINT_SCHEMA ='appserver' AND
      REFERENCED_TABLE_NAME = 'jhi_user';
```

```
# 清除sum
./mvnw compile liquibase:clearCheckSums
```

```shell
# 查看启动了哪些服务
service --status-all |more
```

```
admin/aMki@280  QA

```

```shell
# 命令回退
git reset --hard 目标版本号
# 推送分支
git push origin tagName
```

```
hwang@avantifytech.com
fb3YDhiu
```

```shell
# 设置ss
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'

# 设置代理
git config --global https.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

