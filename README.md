# html-extractor

#### 《基于行块分布函数的通用网页正文抽取算法》-稍许改进，Python实现

在第六届中国软件杯大赛分布式爬虫赛题中，实现了该算法，意图实现新闻、博客类网站正文的自动结构化。比赛提供的测试要求提取的正文一字不差，不能包含多余的不属于正文的内容，也不能少了正文内容。《基于行块分布函数的通用网页正文抽取算法》提取的正文基本正确，但要做到一字不差，却有点困难，于是提出了以下改进。

该正文抽取算法在基于行块分布函数的网页正文抽取方法上做了稍许改进，提高了准确率，使提取的正文更加“一字不差”。在比赛给出的测试包下进行测试，准确率达到90以上。

## 算法实现描述

对于新闻博客类网站，一般文字内容最集中的区域就是正文。但是也不尽然，有些新闻正文很短，而导航栏内容信息很多。首先，过滤噪声标签等的影响。采用正则过滤掉ul、script、style、注释等内容，标记该内容为A，然后过滤所有标签，再标记该内容为B。然后定义k行为一个行块，去掉空格的长度为行块长度。将过滤掉标签的内容B进行行块长度统计，根据行块分布找出最密集的区域则为初步得到的正文内容Text。

该正文内容已经基本正确，但是如果该正文区域后方或前方不远处出现小部分无关内容，也会计入正文内容，导致有稍许误差。为了提高准确率，在去掉噪声的网页A中全文搜索初步正文Text中的块信息，一般为“p“标签，再计算得到该标签的父节点。将所有获得的父节点存储下来，出现次数最多的父节点标签记为包含整个正文区域的标签。直接从该标签提取文字即为正文。该过程失败则使用之前提取的内容Text作为正文，成功则使用该过程提取的文字作为正文。

---

附：《基于行块分布函数的通用网页正文抽取》是哈尔滨工业大学信息检索研究中心陈 鑫 (Xin Chen) 的研究成果，详情在这：[https://code.google.com/archive/p/cx-extractor/](https://code.google.com/archive/p/cx-extractor/)
