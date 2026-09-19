# 数据库内核与系统学习知识库 (Database Learning)

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Database](https://img.shields.io/badge/Focus-Database%20Internals-brightgreen)](https://github.com/gcxixi/database-learning)
[![DDIA](https://img.shields.io/badge/Reference-DDIA%20Practice-orange)](https://dataintensive.net/)

欢迎来到个人数据库学习与内核探索知识库。本项目致力于打通**“经典学术理论（如《DDIA》、CMU 15-445/721）”**与**“工业级生产实战（如云原生网络云盘、现代存储介质经济学、高并发写入内核优化）”**之间的鸿沟，系统化沉淀数据库底层技术、架构选型对比与性能实测分析。

---

## 📚 知识库目录结构与专题索引

### 专题 01：底层存储引擎与现代硬件 (Storage Engines & Hardware)

| 篇章 | 核心议题 | 关键知识点 | 原创度 / 状态 |
| :--- | :--- | :--- | :--- |
| 📖 **[LSM-Tree vs B-Tree 在云盘时代的重构](./topics/01-storage-engines/lsm-vs-btree-cloud-era.md)** | 为什么 VictoriaMetrics 实测 WAF 只有 1.9x？ | DDIA 理论局限、zstd 压缩对冲、Page Cache 截流、Retention 自然消亡、IOPS 与带宽墙经济学 | 深度解构与补充分析 |

### 专题 02：事务与并发控制 (Concurrency Control)

| 篇章 | 核心议题 | 关键知识点 | 原创度 / 状态 |
| :--- | :--- | :--- | :--- |
| 📖 **[Shopify 极限并发库存预占与 MySQL SKIP LOCKED 架构演进](./topics/02-concurrency-control/shopify-inventory-reservations-mysql-skip-locked.md)** | 为什么用 MySQL 替代 Redis 预占能抗住黑五峰值？ | Bounded Unit-Row Pool、`SKIP LOCKED` 行锁消争用、复合聚簇主键单锁优化、`READ COMMITTED` 消除间隙锁、ProxySQL 连接持有时间治理、全场景适用性案例 | 深度解构与全场景推演 |

---

## 📜 优质博文与讨论原案归档 (Original Posts Archive)

知识库完整收录业界专家的高价值技术讨论、深度长文与推特实战溯源：

- 📌 **[2026-05-12 Shopify Engineering: 我们在库存预占中用 MySQL 替换了 Redis —— 而且它成功抗住了超大规模流量 (全译文)](./originals/2026-05-12-shopify-scaling-inventory-reservations-cn.md)**
  - 还原黑五每分钟 510 万美元销售额下的库存防超卖双阶段设计与 GitHub Gist 核心 SQL。
- 📌 **[2026-09-09 包研 (@plantegg): 评《DDIA》与 LSM vs B-Tree 真实生产实测](./originals/2026-09-09-plantegg-lsm-vs-btree.md)**
  - 附带云盘对比图表与 48 万行/秒压测数字推导。

---

## 🧭 数据库知识演进图谱 (Knowledge Roadmap)

```text
database-learning/
├── topics/                        # 深度专题剖析与生产实践复盘
│   ├── 01-storage-engines/        # 存储引擎 (B-Tree, LSM-Tree, Bitcask, Columnar)
│   ├── 02-concurrency-control/    # 事务与并发控制 (MVCC, 2PL, SSI, Snapshot Isolation, SKIP LOCKED)
│   ├── 03-distributed-consensus/  # 分布式系统与一致性 (Raft, Paxos, Spanner, TSO)
│   └── 04-query-execution/        # 查询引擎与优化器 (Volcano, Vectorization, CBO)
├── originals/                     # 业界专家原始优质长推、博文、论文归档
└── docs/                          # 读书笔记 (DDIA, Database Internals, PostgreSQL/MySQL源码)
```

---

## 💡 核心学习方法论

1. **破除单一理论教条**：拒绝“真空中球形奶牛”式的纸面认知，将算法理论带入现代真实 Linux 内核与网络云盘（AWS EBS, 阿里云 ESSD）中进行检验。
2. **算清硬件与经济账单**：衡量存储架构的优劣，不仅要看时间复杂度与理论写放大，更要看云基础设施的**IOPS 配额 vs 带宽 (MB/s) 计费模型**。
3. **基于业务形态找杠杆**：时序、OLTP、OLAP 的读写不对称性是打破学术“不可能三角”（如 RUM 猜想）的最大工程支点。
4. **水暖工程与全链路治理**：高并发瓶颈往往不发生在数据库引擎本身，而发生在连接持有时间与事务编排中。善用连接可见性与代理层治理，让服务成为共享主库的“安全好邻居”。

---

## 📄 License

[MIT](LICENSE)
