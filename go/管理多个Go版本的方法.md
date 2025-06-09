## 1、思路

下载不同版本的 Go 二进制包，通过软链接（Symbolic Link）切换版本，不需要依赖第三方工具，手动可控的管理方式。不足的是需要每次手动操作切换版本的执行命令，这也是有办法的，我们可以写一个简易脚本让其自动化。

## 2、实现

### 2.1 创建 Go 安装目录
首先，我们需要一个统一的目录来存放不同版本的 Go，执行命令：

```bash
# 创建一个目录存放所有的 Go 版本
mkdir -p ~/SoftwareConfiguration/go/versions

# 创建一个目录存放当前使用的 Go 版本（软链接使用）
mkdir -p ~/SoftwareConfiguration/go/current
```
- `~`：指的是 Users/用户名
- `~/SoftwareConfiguration/go/versions`：存放不同版本的 Go（如：go1.23.1、go1.24.4）
- `~/SoftwareConfiguration/go/current`：存放当前使用的 Go 版本（通过软链接指向某个版本）
- `SoftwareConfiguration/go`：我自定义的目录，根据自己需要创建

### 2.2 下载多个版本的二进制包

去官网下载或者运行命令下载均可：

``` bash
# 进去 Go 版本存放目录
cd ~/SoftwareConfiguration/go/versions

# 下载 Go 1.23.1 和 Go 1.24.4
wget https://go.dev/dl/go1.23.1.darwin-amd64.tar.gz
wget https://go.dev/dl/go1.24.4.darwin-amd64.tar.gz

# 解压
tar -zxf go1.23.1.darwin-amd64.tar.gz

# 重命名文件夹
mv go go1.23.1

# 解压
tar -zxf go1.24.4.darwin-amd64.tar.gz

# 重命名文件夹
mv go go1.24.4
```
这样，`~/SoftwareConfiguration/go/versions` 下有两个文件夹 `go1.23.1` 和 `go1.24.4`.

### 2.3 设置软链接

软链接（Symbolic Link）相当于一个快捷方式，我们可以让 `~/SoftwareConfiguration/go/current` 指向某个 Go 版本，这样我们切换版本的时候只需修改这个链接即可。

#### 2.3.1 首次设置软链接

选择当前一个版本，选择其作为使用版本：

```bash
# 删除旧的软链接，一定要删除！！！
rm -rf ~/SoftwareConfiguration/go/current

# 创建软链接，指向 1.24.4
ln -s ~/SoftwareConfiguration/go/versions/go1.24.4 ~/SoftwareConfiguration/go/current
```

现在，`~/SoftwareConfiguration/go/current` 版本代表的是：Go 1.24.4

#### 2.3.2 验证是否成功

```bash
ls -l ~/SoftwareConfiguration/go/current

# 输出
lrwxr-xr-x@ 1 xxxxxx  staff  59  6  8 20:38 /Users/xxxxx/SoftwareConfiguration/go/current -> /Users/xxxxxx/SoftwareConfiguration/go/versions/go1.24.4
```
如果输出类似上面的内容，说明软链接设置成功。

### 2.4 配置环境变量

#### 2.4.1 打开配置文件

使用 zsh，打开 zshrc，使用 bash，则是 bahsrc。

``` bash
open -e ~/.zshrc
```
#### 2.4.2 添加内容

```bash
# Go 的工作目录（存放项目代码和依赖）
export GOPATH="$HOME/Go"
# Go 的 bin 目录加入 PATH
export PATH="$HOME/SoftwareConfiguration/go/current/bin:$PATH"
```
#### 2.4.3 配置生效

```bash
source ~/.zshrc
```

### 2.5 检查版本切换是否成功

```bash
go version
# go version go1.24.4 darwin/amd64
```
如上，说明 go1.24.4 已成功安装并生效。

### 2.6 切换成其他版本（如：go1.23.1）

```bash
# 删除现有软链接
rm -rf ~/SoftwareConfiguration/go/current

# 创建软链接，指向 1.23.1
ln -s ~/SoftwareConfiguration/go/versions/go1.23.1 ~/SoftwareConfiguration/go/current

# 检查版本
go version
# go version go1.23.1 darwin/amd64
```

### 2.7 脚本切换

#### 2.7.1 创建切换脚本

创建空白脚本文件，命名为：go-version-use

```bash
touch ~/SoftwareConfiguration/go/go-version-use
```
#### 2.7.2 脚本内容

```bash
#!/bin/bash
# 用法：go-version-use <版本号>
VERSION=$1
rm -f ~/SoftwareConfiguration/go/current
ln -s ~/SoftwareConfiguration/go/versions/go$VERSION ~/SoftwareConfiguration/go/current
echo "Success,Current Go Version is $VERSION"
```
#### 2.7.3 执行权限

```bash
chmod +x ~/SoftwareConfiguration/go/go-version-use
```
#### 2.7.4 使用脚本切换

```bash
# 进入脚本文件目录
./go-version-use <版本号>
# 如：./go-version-use 1.24.4
```






