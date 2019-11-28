# searchItemRecommend(开坑)
目标: 基于fptree实现文本搜索关联推荐引擎。  
如搜索 牛仔裤，关联出水洗牛仔裤，加绒加厚牛仔裤等。  

#基本实现思路：  
1. 建立业务词库。  
 - 内容资讯型网站： 针对网站sitemap，遍历页面。每个页面，进行句子拆分，再对句子进行分词，形成page_id:sentence_id:words_seq的行记录。
 - 商品类网站： 对仓库item和item tag，生成item_id:item_words的行记录。
 统计清理停用词和无意义词部分。  
2. 基于词库构建fptree，生成word:count:linknode的priority-queue，存入redis作为索引。fptree结构如何在固化在redis中？  
3. 对于客户端进入的搜索词，做文本拆分，得到word-linknode入口，获取topN fptree序列，返回结果。  
搜索词不在词库中如何处理？

4. 新生成的品类/页面，定期维护索引和fptree结构。


