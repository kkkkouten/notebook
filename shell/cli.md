# shell CLI



## 常用命令
### 复制
 `cp` 命令来复制文件到另一个目录里
```shell
cp <source_file> <destination_directory>

# eg
cp file.txt /path/to/destination
```

### 移动
`mv` 命令用于将文件或目录从一个位置移动到另一个位置
```shell
mv <source> <destination>

# eg
mv file.txt /path/to/destination
```



### 生效

`source` 是一个用于加载脚本文件的命令。它会读取指定的脚本文件并在当前的命令环境中执行其中的命令

```shell
# 一般语法
source <filename>

# 等效的缩写形式
. <filename>
```
使用 source 或 . 命令来加载脚本文件时，脚本中的命令会在当前的命令环境中直接执行，而不是创建一个新的子进程来执行脚本。这意味着，脚本中定义的变量、函数或其他命令在加载后会在当前的命令环境中保持有效。

**这在加载环境变量、别名、函数等设置的脚本时非常有用。通过使用 source 命令加载脚本，可以确保所做的更改在当前的命令会话中立即生效。**

需要注意的是，source 命令通常用于特定的Shell环境（例如bash、zsh等），而不是作为通用的命令。因此，在某些Shell或操作系统中，可能使用不同的命令来实现相同的功能



