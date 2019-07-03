# pydensecrf
    https://github.com/lucasb-eyer/pydensecrf
windows下pip install 会报缺少 Microsoft Visual C++ 14.0 用conda  
conda install -c conda-forge pydensecrf

# pickle
import pickle
**output = open('data.pkl', 'wb')**
pickle.dump(object, output)

pkl_file = open('data.pkl', 'rb')
object = pickle.load(pkl_file)

# feather
用于数据框的快速读写



# 压缩
## gzip
    import gzip  
    f = gzip.open('file.txt.gz', 'rb')  
    file_content = f.read()  
    f.close()  
创建gzip文件:
   
    f = gzip.open('file.txt.gz', 'wb')  
    f.write("Lots of content here")  
    f.close()  
gzip压缩现有文件:

    f_in = open('file.txt', 'rb')  
    f_out = gzip.open('file.txt.gz', 'wb')  
    f_out.writelines(f_in)  


# optparse
用于处理命令行参数的库

    from optparse import OptionParser
    parser = OptionParser() 
    parser.add_option("-f", "--file", type="string",action="store", dest="filename", 
                      help="write report to FILE", metavar="FILE")
    parser.add_option("-q", "--quiet",  
                      action="store_false", dest="verbose", default=True,  
                      help="don't print status messages to stdout")  
    (options, args) = parser.parse_args()              

## add_option
* type 默认为’string’
* -- 长参数名 是可选的
* dest 参数也是可选的。如果没有指定 dest 参数，将用命令行的参数名来对 options 对象的值进行存取
* action
    parser.add_option("-v", action="store_true", dest="verbose")  
    parser.add_option("-q", action="store_false", dest="verbose") 
store_const 、append 、count 、callback 
*  metavar 有助于提醒用户，该命令行参数所期待的参数

## parse_args
也可以传递一个命令行参数列表到 parse_args(),默认使用 sys.argv[1:]
* options，它是一个对象（optpars.Values），保存有命令行参数值。只要知道命令行参数名，如 file，就可以访问其对应的值： options.file
* args，它是一个由 positional arguments 组成的列表

# pyqt
anaconda下pip install 会报dll缺失，用conda install 即可
