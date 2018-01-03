# dictionary
## info
* dictionary = corpora.Dictionary(data)
* dictionary = corpora.Dictionary.load(filepath)
* str(dictionary)
* dictionary.num_docs #文档数目  
* dictionary.num_pos #所有词的个数  
* dictionary.num_nnz #每个文件中不重复词个数的和  

## apply
* dictionary.dfs #字典，key,value分别对应{单词id，在多少文档中出现}  
* dict(dictionary.items())) #  字典，{单词id，对应的词} 
* dict(dictionary.id2token) #字典，{单词id，对应的词} dictionary.id2token[id]获取词
* dict(dictionary.token2id) #字典，{词，对应的单词id}
* dictionary.add_documents([b])  

## doc2bow
* result, missing = dictionary.doc2bow(b, allow_update=False,return_missing=True) allow_update->更新当前字典；return_missing->返回字典中不存在的词 result为b文章转换得到的词袋，列表[(单词id，词频)]
 
* result  列表[(单词id，词频)]
* dict(missing)  不在字典中的词及其词频，字典{单词:词频} 

## filter
* dictionary.filter_extremes(no_below=1, no_above=0.5, keep_n=10)  
过滤文档频率大于no_below，小于no_above*num_docs的词
* dictionary.filter_tokens(idlist)

# Models
## tfidf model

