# 推送GitHub步骤

## 一、前提【时间紧迫可以忽略，直接看二】
本文档是《[Bioconda基本使用.md](https://github.com/yanghanchi/bioconda_tmp)》中，第12步的详细步骤展开。

一般公司服务器已经安装好了Git版本控制工具，如果毫无Git使用经验，建议快速观看B站完整课程，单看示例命令行可以完成，但是非常难以理解。

注意：大多操作有严格的先后顺序，否则容易出现报错；尤其是多人协同开发场景下，切记先pull（保持同步）再push（推送）。

代码文件已修改好；软件已经验证成功。

验证方法在meta.yaml文件的test中，一般是
```
R -e "library('软件name')"
```
软件name在package下的name中

## 二、准备工作
### 1.在自己的GitHub账号生成token

原因：

GitHub不再支持用户名密码的方式连接，需要使用token方式。

路径：

GitHub页面右上角自己的头像->settings->developer settings->personal access tokens->tokens(classic)
->generate new token：根据个人偏好填写设置并生成->本地保存token

### 2.添加远程仓库
与自己的远程库对接

```
git remote add <远端名称> <仓库路径>
```
设置远程仓库下次连接不再需要输入密码
```
git remote set-url origin https://<你的token>@github.com/<你的GitHub账户名>/<你想要推送的GitHub仓库名>.git
```
**备注：**

远端名称默认是origin，为后续操作方便，建议不要起其他名称

远程仓库路径查询
```
git remote -v
```
删除远程仓库
```
git remote rm <远端名称>
```
3.创建并切换到新分支

```
git branch <分支名>
```

```
git checkout <分支名>
```
**备注：**

分支名设置为当前软件名称

删除分支
```
git branch -d <分支名> #不能删除当前分支，切换后再删除
```
常见报错解决：

切换分支后再切回

## 三、提交
### 1.提交
```
git add <文件名>
```
```
git commit -m "注释内容"
```
**备注：**

注释内容一般是软件名称

查看提交日志
```
git log
```
撤销add（从暂存区中移除）
```
git reset <文件名>
```
版本回退（commit后形成版本）
```
git reset [--hard commitID]
```
### 2.推送至GitHub
```
git push [-f][--set-upstream][远端名称[本地分支名][:远端分支名]]
```

**备注：**

-f 表示强制覆盖

--set-upstream 推送到远端的同时并且建立起和远端分支的关联关系

经过以上正确配置，根据下图操作即可完成
 ![](./images/1717124374346_image.png)
常见报错解决：

GitHub经常出现报错，尝试再次push

GitHub timeout: 删除远程仓库，再次添加

## 四、pull request
推送成功后，自己的GitHub仓库页面一般会出现绿色按钮pull request&compare

点击之后填写题目和内容，附上验证成功图片，create，全部流程完成。

备注：

没有绿色按钮时，可以点击下图中contribute中的绿色按钮

![](./images/1717126883412_image.png)
已创建的pull request页面中可以编辑题目和内容

最下方可以close，点击最下方提交记录可以查看与原代码的compare
![](./images/1717127052411_image.png)
在代码仓中查看其他人的pull request
![](./images/1717127139218_image.png)

## 五、其他
anaconda安装和git clone的代码仓建议直接放在/root目录下
