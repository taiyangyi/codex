## 1、设置 Git 的 user.name 和 user.email

如果 git 新安装，没有设置 `user.name` 和 `user.email`，先设置好自己的。

```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱地址"
```

## 2、检查本地电脑是否有 ssh key

已安装好的 git，windows 系统鼠标右键，打开 `git bash`，输入 `~/.ssh` 查看电脑是否存在 `.ssh` 文件夹。此时会出现两种结果：

```
# bash: /c/Users/电脑用户名/.ssh: Is a directory
表示已存在

# bash: /c/Users/电脑用户名/.ssh: No such file or directory
表示不存在
```

如果已经存在 `.ssh` 文件夹，表示我们不再需要创建 `ssh key`，可以跳过步骤三。不存在，则需要创建 `ssh key`

## 3、创建 ssh key

在创建过程中提示输入密码，直接回车两次，不然设置了密码，在 `ssh` 传输的时候每次都得输密码。

```
ssh-keygen -t rsa -C "你的邮箱地址" (和git的email 保持一致)
```

创建 `ssh key` 会默认生成两个秘钥文件：`id_rsa` 和 `id_rsa.pub`，判断是否已经创建成功，使用 `~/.ssh`,就会提示你 `bash: /c/Users/电脑用户名/.ssh: Is a directory`，当然内容的信息给你提供了文件所在的位置：`/c/Users/电脑用户名/.ssh`。

## 4、添加 ssh key 到 github

进入 `github` 主页，点击头像找到 `Settings` 选择 `SSH and GPG keys`，点击右上角按钮 `New SSH key`：

- Title：填写 title，建议备注好名称，方便区分以及后期准备删除，防止误删；
- Key：打开 `id_rsa.pub` 文件，将里面的内容全部粘贴复制到这里；

此时，就完成了。

## 5、验证是否成功

打开 `git bash`输入：`ssh -T git@github.com`，提示是否继续连接，输入 `yes`。出现已下提示，表示我们已经连接成功。

```
Hi 用户名！You've successfully authenticated，but GitHub does...
```

