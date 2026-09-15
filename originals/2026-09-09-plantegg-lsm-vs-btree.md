# 哇，评论区给了我很多深入理解这本书的导火索，比如两种存储 LSM VS B-Tree

[![Author](https://img.shields.io/badge/Author-@plantegg-1DA1F2?logo=x&logoColor=white)](https://x.com/plantegg) [![Original Post](https://img.shields.io/badge/X-View%20Post-black?logo=x&logoColor=white)](https://x.com/plantegg/status/2097539229551346147) [![Type](https://img.shields.io/badge/Format-Note%%20Tweet%%20(Long)-purple) ](https://x.com/plantegg/status/2097539229551346147) 

## 👤 作者信息 (Author Profile)

- **作者**: plantegg ([@plantegg](https://x.com/plantegg)) ✓ (Verified)
- **简介**: Claude code/AI/Agent/智能体，AI探索，云计算专家，云资源优化专家
- **发布时间**: `Wed Sep 09 04:14:57 +0000 2026`
- **原文链接**: <https://x.com/plantegg/status/2097539229551346147>

### 📊 互动数据 (Engagement Stats)

| 浏览量 (Views) | 喜欢 (Likes) | 转发 (Reposts) | 书签 (Bookmarks) | 回复 (Replies) |
| :--- | :--- | :--- | :--- | :--- |
| 13926 | 100 | 12 | 99 | 142 |

---

## 📝 正文内容 (Post Content)

哇，评论区给了我很多深入理解这本书的导火索，比如两种存储 LSM VS B-Tree

  DDIA 是好书，但只读书你会得出一个错误结论。我这次带入了我实践中碰到的 VictoriaMetrics 打满云盘带宽扩容的案例，理解起来就好多了

  Kleppmann 说 LSM-Tree 写放大理论值 10-30x，B-Tree 更"可预测"。读完你可能觉得 LSM是个不得已的妥协——为了写入性能，忍受了一个巨大的隐性成本。

  这个理解放到 2015 年的 HDD 时代是对的。放到今天的云盘时代，差了一个数量级。

  我们生产环境 VictoriaMetrics 集群（LSM 引擎），12 节点，每节点 48 万行/秒写入，45 天实测 WAF 只有1.9x。不是 10x，不是 20x，是 1.9x。

  原因：zstd 压缩比 6:1（时序数据高度规律），128GB 内存带来极高 page cache 命中率（merge 读几乎不落盘），retention 过期让数据在低层级自然消亡不触发深层 compaction。

这些工程因素 DDIA 一个都没讲，但它们把理论写放大砍掉了一个数量级。

  书上的理论模型是"球形奶牛"——真空中的 WAF。

比如现在几乎都用云盘了，iops不要钱且超大、bps极其珍贵，1T云盘免费有5万iops、350Mb的带宽

DDIA 说 "LSM 对顺序 IO 友好" 的优势在云盘上缩小了，但没有消失。

### 🖼️ 附带媒体 (Attached Media)

![Attached Image 1](https://pbs.twimg.com/media/HRv0DHOb0AAuxVP.jpg?name=orig)



---

## 💬 引用推文 (Quoted Posts)

> ### 引用: plantegg ([@plantegg](https://x.com/plantegg))
> **时间**: `Tue Sep 08 07:52:14 +0000 2026` | [原文链接](https://x.com/plantegg/status/2097231522466042296)
>
> 这本居然有9.6分的书，谁能给我讲1-3点从中学到的知识点？
> 
> 我去学习下，谢谢 https://t.co/S6BC3sEhFF


