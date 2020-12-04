# LinuxCommand

## apt
### 清除配置和依赖
```shell
sudo apt-get autoremove --purge goldendict
- autoremove 清除依赖
- --purge
```

## 解压
### unrar  不带后面参数就是不按目录结构解压
```shell
unrar x -o- -y
```
### zip
将压缩文件text.zip在指定目录/tmp下解压缩，如果已有相同的文件存在，要求unzip命令不覆盖原先的文件。
```shell
unzip -n test.zip -d /tmp
```

## 端口

### 查看端口占用
```shell
netstat -anp |grep 端口号
```

## 传输
### SFTP
```shell
sftp -P 32122 47.112.***.***
```

### SCP
```shell
scp -r 文件  主机名@ip：/存放目录
```

### cat
```shell
cat log.txt | grep 'ERROR' -B 5  之前5行

cat log.txt | grep 'ERROR' -C 5 前后5行

cat log.txt | grep -v 'ERROR' 排除ERROR所在的行
```

##curl

### https
```shell
执行curl命令
１、使用client.pem+key.pem
curl -k --cert client.pem --key key.pem https://www.xxxx.com
```

2、使用all.pem
```shell
curl -k --cert all.pem https://www.xxxx.com
```

## 权限
### 可执行文件 .sh
find ../bin -name "*.sh" -exec chmod a+x {} \;

## mysql
```shell
mysql -u 用户名 -p
```
