忘记密码了怎么办  
=====
## 适用情况  
* 1、第一次安装mysql未给出密码设置向导，导致不知道密码与用户名，需要重置；    
* 2、忘记密码;  

## 进入文件
```Linux
sudo cat /etc/mysql/debian.cnf 
user = debian-sys-maint
userpasswod = xxxx
```


## 于  是
```Linux
：mysql -udebian-sys-maint -pxxxx
```


##　在mysql下输入
```Linux
mysql: use mysql; 
mysql: update mysql.user set authentication_string=password('123456') 
		  where user='root' and Host ='localhost'; 
mysql: update user set  plugin="mysql_native_password";     
mysql: flush privileges;
mysql: quit; 
```

