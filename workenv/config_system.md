# windows
## sublime
通过 ctrl+` 快捷键或者 View > Show Console菜单打开控制台
快捷键 Ctrl+Shift+P（菜单 – Tools – Command Paletter），输入 install 选中Install Package并回车，输入或选择你需要的插件回车

## pycharm
### deployment
首先我们需要配置PyCharm通服务器的代码同步，打开Tools | Deployment | Configuration
点击左边的“+”添加一个部署配置，输入名字，类型选SFTP
确定之后，再配置远程服务器的ip、端口、用户名和密码。root path是文件上传的根目录，注意这个目录必须用户名有权限创建文件。
然后配置映射，local path是你的工程目录，就是需要将本地这个目录同步到服务器上面，我填的是项目根目录。 Deploy path on server 这里填写相对于root path的目录，下面那个web path不用管先
如果你还有一些文件或文件夹不想同步，那么在配置对话框的第三个tab页“Excluded path”里面添加即可，可同时指定本地和远程。
还有一个设置，打开Tools | Deployment | Options，将”Create Empty directories”打上勾，要是指定的文件夹不存在，会自动创建。
手动上传方式很简单，选择需要同步的文件或文件夹，然后选择 Tools | Deployment | Upload to sftp(这个是刚刚配置的部署名称)
选择Tools | Deployment | Browse Remote Host，打开远程文件视图，在右侧窗口就能看到远程主机中的文件
配置远程Python解释器
选择File | Settings，选择Project | Project Interpreter

## sumatra pdf
应运行的命令框中输入："C:\Program Files\Sublime Text 3\sublime_text.exe" "%f:%l"

## XX-net
### 代理模式
“全局PAC智能代理“，这个选项他的意思就是他会一次性修改windows操作系统的统一的代理服务器设置参数，那么很多程序，如果遵循这个proxy设置（特别是用WinHTTP这个库编程的），就其实已经翻墙了，无需设置，具体来讲，XX-Net会建立一个本地的代理服务器，默认是127.0.0.1:8086，这个服务器提供一个PAC脚本，用脚本的原因是可以灵活处理哪些域名走代理，哪些不走。
 
“取消全局代理”，这个选项只是取消windows系统一级的代理设置，但是XX-Net本身会在本地建立127.0.0.1:8087这个代理端口，程序只要把代理服务器设置为这个地址，就可以通过这个地址和端口上网，这个和全局代理基本上没什么区别，区别可能在于哪些网站走代理，哪些不走，这个时候需要XX-Net来判断，而不是WinHTTP或者你想要用来上网的程序，比如chrome浏览器

## docker toolbox install 
* docker-machine create --driver=virtualbox default boot2docker.iso可以直接从github下载https://github.com/boot2docker/boot2docker/releases/，复制到C:\Users\Administrator\.docker\machine\cache下

*  docker-machine env default 获得虚拟机的环境变量

*  docker-machine env default | Invoke-Expression 把当前的PowerShell和虚拟机里面的Docker Linux建立的连接
*   DAO加速器 https://www.daocloud.io/mirror#accelerator-doc
sudo sed -i "s|EXTRA_ARGS='|EXTRA_ARGS='--registry-mirror=mirror地址 |g" /var/lib/boot2docker/profile




