[TOC]
# os
## basic
* os.name()——判断现在正在实用的平台，Windows 返回 ‘nt'; Linux 返回’posix'
* os.getcwd()——得到当前工作的目录。
* os.listdir(path)——指定所有目录下所有的文件和目录名。
* os.remove()——删除指定文件
* os.rmdir()——删除指定目录
* os.chdir()——改变目录到指定目录
* os.mkdir()——创建目录 **注意**这样只能建立一层，要想递归建立可用：os.makedirs()
* os.system()——执行shell命令。
* os.getgruops() 得到用户组名称列表 
* os.getlogin() 得到用户登录名称 
* os.getenv 得到环境变量 
* os.putenv 设置环境变量

## path
* os.path.isfile()——判断指定对象是否为文件。是返回True,否则False
* os.path.isdir()——判断指定对象是否为目录。是True,否则False。
* os.path.exists()——检验指定的对象是否存在。是True,否则False.例：
* os.path.split()——返回路径的目录和文件名。
此处只是把前后两部分分开而已。就是找最后一个'/'。
* os.path.join(path, name) 注意name前面不能有'/'，否则得到的值为name本身
* os.path.getsize()——获得文件的大小，如果为目录，返回0
* os.path.abspath()——获得绝对路径
* os.path.basename(path)——返回文件名
* os.path.dirname(path)——返回文件路径
 

## os.walk()
    for dirpath,dirnames,filenames in os.walk():
dirpath 是一个string，代表目录的路径，
dirnames 是一个list，包含了dirpath下所有子目录的名字。
filenames 是一个list，包含了非目录文件的名字。

# sys
* sys.argv 参数list
* sys.exit() 退出
* sys.path 获取指定模块搜索路径的字符串列表,sys.path.append(path)来添加
* sys.modules 全局字典记录模块
* sys.stdout.write(obj+'\n') print 调用该方法


# pathlib
## Structure
* Path
* PurePath
* PurePosixPath
* PureWindowsPath
* PosixPath
* WindowsPath

## Path
* p = Path('.') 
* [x for x in p.iterdir() if x.is_dir()]
* q.exists()
* q.is_dir()
* with q.open() as f: f.readline()
* list(p.glob('*\*/\*.py'))
* q = p / 'init.d' / 'reboot'

## PurePath
*  parents
p = PureWindowsPath('c:/foo/bar/setup.py')
p.parents[0]
PureWindowsPath('c:/foo/bar')
p.parents[1]
PureWindowsPath('c:/foo')
p.parents[2]
PureWindowsPath('c:/')
* parent 等于parents[0]
* PurePath.name
* PurePath.suffix
* PurePath.stem 没有后缀
* PurePath.as_posix()
* PurePath.as_uri()
* PurePath.is_absolute()
* PurePath.match(pattern)
* PurePath.joinpath(*other)
