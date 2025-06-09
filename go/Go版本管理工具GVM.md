## 1、GVM

GVM 是 Go Version Manager 的缩写，它是一个用于管理多个 Go 语言版本的工具。GVM 允许你在同一台机器上安装和切换不同的 Go 版本。对于开发者而言，可以轻松切换和管理不同版本的 Go，以满足不同项目的需求。

## 2、Homebrew 安装 GVM

```
sh < <(curl -s https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

## 3、确认 GVM 安装位置
```
which gvm
```

## 4、初始化 GVM

shell 配置文件（如 ​​​~/.bash_profile​​​ 或 ​​~/.zshrc​​）中添加：

```
source "$HOME/.gvm/scripts/gvm"
```

执行：
```
source ~/.bash_profile  # 或 source ~/.zshrc
```

## 5、GVM 版本

```
gvm version
```

## 6、常用命令

### 6.1 列出可用的 Go 版本

```
gvm listall
```

## 6.2 安装 Go 版本
```
gvm install go1.23.1
```

### 6.3 查看已安装的版本

```
gvm list
```

## 6.4 使用特定版本

```
gvm use go1.23.1
```

## 6.5 设置默认的 Go 版本

```
gvm use go1.23.1 --default
```

## 6.6 卸载特定版本

```
gvm uninstall go1.17.6
```

## 6.7 查看当前使用的版本

```
go version
```

