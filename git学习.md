# 常见git命令/操作以及git远程仓库的使用

## 1.安装git并生成ssh公钥

安装过程略

生成ssh公钥命令

```javascript
ssh-keygen -t rsa -C "你的邮箱地址"
```

生成结果

![image-20220207191156486](D:\document\notebook\image-20220207191156486.png)

配置windows凭据

![image-20220207191409206](D:\document\notebook\image-20220207191409206.png)

## 2.注册github账号并添加ssh公钥

注册过程略

添加ssh公钥

![image-20220207191528903](D:\document\notebook\image-20220207191528903.png)

创建一个新的仓库

![image-20220207191603386](D:\document\notebook\image-20220207191603386.png)

创建之后有如下提示

```java
echo "# testwang" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin git@github.com:shenjipo/testwang.git
git push -u origin master
```

## 3.将本地某个文件夹交给git管理

在该文件夹的地址栏中输出cmd打开命令行窗口，依次输入如下命令

```java
git init //初始化git仓库
git add . //
git commit -m "初始化项目"
git remote add origin git@github.com:shenjipo/testwang.git  //设置远程仓库地址
git push -u origin master   //提交到远程仓库
```

![image-20220207192129401](D:\document\notebook\image-20220207192129401.png)

## 4.更新文件内容并同步到远程仓库

修改好内容

```java
git add .
git commit -m "修改结束"
git push origin master:master //git push <远程主机名> <本地分支名>:<远程分支名>
```



## 5.在IDEA中使用git(图形化界面)以及冲突的处理

1.git初始化仓库

![image-20220207200928833](D:\document\notebook\image-20220207200928833.png)

2.上传到远程仓库

![image-20220207201217334](D:\document\notebook\image-20220207201217334.png)

![image-20220207201459483](D:\document\notebook\image-20220207201459483.png)

3.冲突的处理

3.1dev修改了wang_test.js如下内容

```javascript
let a = 1
let b = 5

let c = 5
let d = 6
```

3.2master修改了wang_test.js如下内容

```javascript
let a = 1
let b = 5

let e = 7
let f = 8
```

3.3合并解决冲突

![image-20220207202043998](D:\document\notebook\image-20220207202043998.png)

显示冲突的文件，双击进行人工解决冲突

![image-20220207202122624](D:\document\notebook\image-20220207202122624.png)

![image-20220207202130708](D:\document\notebook\image-20220207202130708.png)

3.4解决完成 提交到远程仓库

解决之后查看Log，可以明显看到解决冲突

![image-20220207202254222](D:\document\notebook\image-20220207202254222.png)

## 6.总结



