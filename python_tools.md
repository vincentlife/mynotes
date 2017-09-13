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

* pip show
* pip search "query"

# conda


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
Out[2]: 'sha1:ce23d945972f:34769685a7ccd3d08c84a18c63968a41f1140274' # 生成hash值
这里如果无法打开ipython，可以直接用命令行
root@docker_admin:~# python -c "import IPython;print IPython.lib.passwd()" 
3. 修改config文件
~/.jupyter/jupyter_notebook_config.py
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha:ce...刚才复制的hash'
c.NotebookApp.open_browser = False 
c.NotebookApp.port =8888

# setuptools

