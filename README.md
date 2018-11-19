svn服务器的搭建
=======================================
```
1、
  创建svn目录
  mkdir /Users/guopp/svn
2、
  创建svn代码库
  svnadmin create /Users/guopp/svn/repository
3、
  修改confg
    a)svnserve.conf:去掉#
      anon-access = read //匿名时候是只读的
      auth-access = write 
    
      authz-db = authz
     b)配置passwd：
     
        username=password
         
     c)配置authz文件
        user=guopp
        [/]
        @user=rw
        
        在[groups]下添加uesrs = guopp 创建了一个用户 
        [/] 
        @users = rw 这两句标示给users用户组相应的权限 
        [/]表示授权的目录路径，这里是根目录，假如根目录下有一个目录叫做test,那么我们如果要编辑此目录的权限那么就要写成[test:/] 
        @uesr表示给用户组授权，如果要给某一个用户授权则不用写前面的@ 
        r表示可读，w表示可写 
        
       d)启动svn服务：
          svnserve -d -r /Users/guopp/svn
          
4、配置Cornerstone
    添加代码库，配置svn server
    server：本地localhost 局域网其他IP地址
    path：svn代码库的地址；

5、从本地导入代码到服务端
    svn import /Users/guopp/project/weChartPublicNumber/weChartProjects svn://localhost/repository/weChatProject 
    --username=guopp --password=1029 -m "初始化导入"

6、从服务端下载代码到客户端本地
     svn checkout svn://localhost/repository/weChatProject 
     --username=guopp --password=1029 /Users/guopp/myProject
    
 7、代码提交和更新
    定位到文件目录；
    svn commit -m "提交描述"；（类似git）
    svn update；
    svn help；
```


