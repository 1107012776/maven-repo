# maven-repo
个人Java的maven仓库

原文:

https://www.cnblogs.com/8hao/p/5390534.html

deploy到本地目录
把本地目录提交到gtihub上
配置github地址为仓库地址
配置local file maven仓库
deploy到本地
maven可以通过http, ftp, ssh等deploy到远程服务器，也可以deploy到本地文件系统里。

例如把项目deploy到/home/hengyunabc/code/maven-repo/repository/目录下：

```
<distributionManagement>
    <repository>
      <id>hengyunabc-mvn-repo</id>
      <url>file:/home/hengyunabc/code/maven-repo/repository/</url>
    </repository>
  </distributionManagement>
  
```
通过命令行则是：
```
mvn deploy -DaltDeploymentRepository=hengyunabc-mvn-repo::default::file:/home/hengyunabc/code/maven-repo/repository/
```
推荐使用命令行来deploy，避免在项目里显式配置。

https://maven.apache.org/plugins/maven-deploy-plugin/

https://maven.apache.org/plugins/maven-deploy-plugin/deploy-file-mojo.html

把本地仓库提交到github上
上面把项目deploy到本地目录home/hengyunabc/code/maven-repo/repository里，下面把这个目录提交到github上。

在Github上新建一个项目，然后把home/hengyunabc/code/maven-repo下的文件都提交到gtihub上。

```
cd /home/hengyunabc/code/maven-repo/
git init
git add repository/*
git commit -m 'deploy xxx'
git remote add origin git@github.com:hengyunabc/maven-repo.git
git push origin master
```
最终效果可以参考我的个人仓库：

https://github.com/hengyunabc/maven-repo

github maven仓库的使用
因为github使用了raw.githubusercontent.com这个域名用于raw文件下载。所以使用这个maven仓库，只要在pom.xml里增加：

<repositories>
        <repository>
            <id>hengyunabc-maven-repo</id>
            <url>https://raw.githubusercontent.com/hengyunabc/maven-repo/master/repository</url>
        </repository>
</repositories>
