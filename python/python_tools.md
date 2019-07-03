# pip
* pip install name /name.whl /url
* pip install --upgrade
* pip uninstall
* pip install -r requirements.txt 
* pip install --user
pip install --user follows four rules:

    - When globally installed packages are on the python path, and they conflict with the installation requirements, they are ignored, and not uninstalled.

    - When globally installed packages are on the python path, and they satisfy the installation requirements, pip does nothing, and reports that requirement is satisfied (similar to how global packages can satisfy requirements when installing packages in a --system-site-packages virtualenv).

    - pip will not perform a --user install in a --no-site-packages virtualenv (i.e. the default kind of virtualenv), due to the user site not being on the python path. The installation would be pointless.

    - In a --system-site-packages virtualenv, pip will not install a package that conflicts with a package in the virtualenv site-packages. The --user installation would lack sys.path precedence and be pointless. 

安装到 $HOME/.local 路径下

* pip show
* pip search "query"

# conda
* conda create -n env_name numpy matplotlib python=3.6
* conda remove -n env_name --all
* activate env_name
* deactivate env_name
* conda install -n env_name pandas
* conda list
* conda list -n env_name 指定查看某环境下安装的package
* conda remove numpy
* conda update numpy
* conda search numpy

## 配置镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

# juypter
## run 
jupyter notebook 
## 远程访问
1. 生成配置文件
$jupyter notebook --generate-config
2. 生成密码
打开ipython，创建一个密文的密码：
In [1]: from notebook.auth import passwd 
In [2]: passwd()
Enter password:  
Verify password:  
Out[2]: 'sha1:ce23d945972f:34769685a7ccd3d08c84a18c63968a41f1140274' # 
生成hash值
这里如果无法打开ipython，可以直接用命令行
root@docker_admin:~# python -c "import IPython;print IPython.lib.passwd()" 
3. 修改config文件
~/.jupyter/jupyter_notebook_config.py
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha:ce...刚才复制的hash'
c.NotebookApp.open_browser = False 
c.NotebookApp.port =8888

## ipykernel
为jupyter增加新的内核
在要增加的python环境下输入

    python -m ipykernel install --user --name myenv --display-name 'Python(myevn_)"
 --name 是给jupyter 启动Kernel 使用，如果指定的name已存在则会覆盖，--display-name 是为Jupyter notebook 菜单显示

## jupyter theme
pip install --upgrade jupyterthemes
jt - l 查看主题
jt -t 主题名称 使用主题
jt -r 恢复默认

## magic methods

1. %：行 Magic 命令， 仅应用于编写 Magic 命令时所在的行；
2. %%：cell Magic 命令， 应用于整个cell (单元格)；
3. 把不同内核的代码结合到一个notebook里运行。
只需在每个单元格的起始，用Jupyter magics调用kernal的名称：
%%bash %%HTML %%python2 %%python3 %%ruby %%perl

* %matplotlib inline
* %who
* %%time cell内代码的单次运行时间信息。
* %%timeit 运行多次取最短
* %%writefile XX.py 保存cell内容到外部文件
* %pycat 显示外部脚本的内容
* %prun 程序中每个函数消耗的时间 
* %pdb 


# setuptools
distutils 打包工具
easy_install 安装工具

wheel本质上是一个 zip 包格式，用于代替egg

Python setup.py [command]
## command
* 固有命令(继承Command类)
    build
    build_ext 
    install
    bdist_egg
    bdist_wheel (需要安装wheel包) 打包成wheel格式
* 自定义命令
继承Command类
    继承上述类，调用父类的run方法

## setup
bdist_wheel调用过程：

* 调用build，其中build _ext完成cython代码的编译  
* 调用install  将dependencies 、版本、文件位置等信息写入egg-info 完成wheel打包

1 ext_modules 
  参数不传或传入列表为空时将按纯python进行操作
  可以通过修改build_ext的子类中的extensions属性来修改

2. packages 
  参数不传或传入列表为空时py文件将不会被打包
  可以用setuptools.find_packages()来找到所有含有__init__.py文件的包

## tqdm




