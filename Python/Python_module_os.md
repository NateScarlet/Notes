[TOC]

# os 模块

## 函数
```
listdir(路径)
返回路径内容列表
getcwd()
返回当前工作目录
getenv('变量名')
获取系统环境变量
chdir()
改变工作目录
makedirs()
创建目录(包括父级)
mkdir()
创建目录
system('命令')
使用系统提示符命令
stat(文件名, *, dir-fd=none, follow_symlinks=True)
返回文件属性
	st_mtime修改时间
```

# os.path 模块

## 函数

```
abspath( 路径 )
返回路径的绝对路径版本
basename( 路径 )
返回路径中的最底层名称
dirname( 路径 )
返回路径目标所属文件夹的路径
exists( 路径 )
返回路径是否存在
expanduser( 路径 )
返回将linux下的~相对用户路径转为绝对路径后的路径
expandvar( 路径 )
返回将路径中的变量转换为变量内容后的路径
getatime( 文件名 )
返回文件的最后访问时间
getctime( 文件名 )
返回文件的创建时间
getmtime( 文件名 )
返回文件的修改时间
isabs( 路径 )
splitext()
splitdrive(字符串)
返回分割的两个字符串，分别为盘符和剩余部分
normcase(字符串)
用两个反斜杠替换斜杠并将所有字母小写
join(a, *p)
连接多个路径
commonprefix( 文件名列表 )
返回列表中最长的共通前缀
```

