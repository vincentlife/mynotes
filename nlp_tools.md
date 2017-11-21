# jieba
支持三种分词模式：
* 精确模式，试图将句子最精确地切开，适合文本分析；
* 全模式，把句子中所有的可以成词的词语都扫描出来, 速度非常快，但是不能解决歧义；
* 搜索引擎模式，在精确模式的基础上，对长词再次切分，提高召回率，适合用于搜索引擎分词。
## jieba.cut 
方法接受三个输入参数: 
* 需要分词的字符串；待分词的字符串可以是 unicode 或 UTF-8 字符串、GBK 字符串。注意：不建议直接输入 GBK 字符串，可能无法预料地错误解码成 UTF-8。
* cut_all 参数用来控制是否采用全模式
* HMM 参数用来控制是否使用 HMM 模型。
## jieba.cut_for_search 方法接受两个参数：
* 需要分词的字符串；
* 是否使用 HMM 模型。该方法适合用于搜索引擎构建倒排索引的分词，粒度比较细。

##  jieba.lcut & jieba.lcut_for_search 
直接返回 list。

## jieba.Tokenizer(dictionary=DEFAULT_DICT)
新建自定义分词器，可用于同时使用不同词典。jieba.dt为默认分词器，所有全局分词相关函数都是该分词器的映射。

# THULAC
pip install thulac

## thulac.thulac() 
thulac(user_dict=None, model_path=None, T2S=False, seg_only=False, filt=False)初始化程序，进行自定义设置
* user_dict
设置用户词典，用户词典中的词会被打上uw标签。词典中每一个词一行，UTF8编码
* T2S                 默认False, 是否将句子从繁体转化为简体
* seg_only            默认False, 时候只进行分词，不进行词性标注
* filt                默认False, 是否使用过滤器去除一些没有意义的词语，例如“可以”。
* model_path          设置模型文件所在文件夹，默认为models/
## cut
cut(文本, text=False) 对一句话进行分词
* text 默认为False, 是否返回文本，不返回文本则返回一个二维数组([[word, tag]..]),seg_only模式下tag为空字符。
## cut_f(输入文件, 输出文件) 
对文件进行分词
## run() 
命令行交互式分词(屏幕输入、屏幕输出)
