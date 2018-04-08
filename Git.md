# Git

安装后配置

```bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

选择一个合适的文件夹，把这个目录变成Git可以管理的仓库。

```bash
git init
```

用命令`git add`把文件添加到仓库：

```bash
git add readme.md
git add file2.txt file3.txt
```

用命令`git commit`告诉Git，把文件提交到仓库,`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的：

```bash
git commit -m "write a readme file"
```

## 远程仓库

### 创建 SSH Key

```bash
ssh-keygen -t rsa -C "youremail@example.com"
```

可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

登陆 GitHub，打开 “Settings”，“SSH Keys”页面；然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。

#### 添加远程库

登陆 GitHub，然后，创建一个新的仓库 test，根据 GitHub 的提示，在本地的仓库下运行命令：

```bash
git remote add origin git@github.com:GitAccountName/test.git
```

下一步，就可以把本地库的所有内容推送到远程库上，后面继续提交只需要这个命令：

```bash
git push -u origin master
```
