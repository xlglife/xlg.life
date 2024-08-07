---
{"dg-publish":true,"dg-permalink":"growup100/050-RPA抓图遇到live图&飞书多维表格与普通表格","permalink":"/growup100/050-RPA抓图遇到live图&飞书多维表格与普通表格/","tags":["小洛哥成长笔记"],"noteIcon":"1","created":"2024-06-08","updated":"2024-06-08"}
---


> 大家好，我是小洛哥，一个刚刚开始每天写作的新人。
> 
> 日更 100 天，第 50 天。

## 01 处理 RPA 抓小红书图片遇到 live 图片的问题

我经常用 RPA 去抓小红书的笔记详情，原本自己写的这个指令已经很稳定了，除了网络问题很久没报错过了。

没想到今早居然遇到一条报错，研究了好久才找到原因在哪。

大概情况是，我需要将小红书的笔记图片下载下来转换为本地图片，然后再上传到飞书多维表的附件字段里（附件字段不允许直接贴网络图片）

平时下载的都是 webp 格式，然后我将格式改为 jpg 后，再去上传。可今天在上传这一步时报错找不到文件。

看了半天日志，也没搞清楚是啥情况。

后来打开原始笔记一看，原来是 live 图片...按照原先的抓图逻辑会把封面图和一个 blob 文件下载下来，然后 blob 文件无法转换成 jpg 格式，自然就找不到文件报错了。

所以，问题是找不到文件，而原因是抓取图片逻辑的正则写的不严谨。

发现正常的 webp 格式图片都是 `http://` 开头的，而 blob 地址是 `https://`。

所以就简单了，正侧由 `http[^"&]+`，改成 `http://[^"&]+`，测试完美，搞定上线！

## 02 飞书多维表格 VS 普通的在线表格

在影刀的飞书相关操作中，有多维表格和在线表格两个选择。

我个人是使用多维表格比较多，因为他可以满足我约束格式、自动化、切换视图等多种需求。慢慢的也养成了我所有表格基本上都用多维表格的习惯。

可今天在思考一个问题时，发现这样是不对的，究竟使用哪种表格，更多的还是要看使用的场景和用途。

为了搞清楚后续在使用时该如何选择，我请 Kimi 参考 [飞书的官方文档](https://www.feishu.cn/hc/zh-CN/articles/501142825365-%E5%8C%BA%E5%88%86%E7%94%B5%E5%AD%90%E8%A1%A8%E6%A0%BC%E4%B8%8E%E5%A4%9A%E7%BB%B4%E8%A1%A8%E6%A0%BC)，帮我列举了一些考虑因素，并做了对比：

| 序号 | 考虑因素          | 多维表格                           | 普通在线表格           |
| ---- | ----------------- | ---------------------------------- | ---------------------- |
| 1    | 功能丰富度        | 高级数据处理、自动化流程、数据可视化 | 基本数据处理、图表生成 |
| 2    | 协作能力          | 实时多人协作、共享，适合团队项目 | 多人协作，但可能不如多维表格实时 |
| 3    | 自动化            | 支持构建自动化流程                 | 通常不支持或功能有限    |
| 4    | 集成性            | 易于与其他应用集成                 | 集成性可能较弱          |
| 5    | 易用性            | 功能丰富，但学习曲线较陡           | 易于使用，适合初学者    |
| 6    | 普及度            | 相对较新，普及度较低               | 广泛使用，用户基础广泛  |
| 7    | 成本              | 可能较高，提供高级功能             | 通常免费或成本较低      |
| 8    | 兼容性            | 可能有限，但专为集成设计           | 支持广泛的文件格式      |
| 9    | 移动办公          | 支持多平台同步                     | 也支持多平台            |
| 10   | 数据安全          | 通常有高级安全措施                 | 安全性取决于服务提供商  |
| 11   | 学习曲线          | 需要时间学习和适应                 | 简单直观，学习成本低    |
| 12   | 市场扩展机会      | 随远程工作和协作需求增加，使用场景更广泛 | 市场成熟，用户接受度高 |
| 13   | 技术更新          | 需要不断更新以满足用户需求         | 更新可能不够及时        |
| 14   | 竞争对手          | 面临其他在线协作工具的竞争         | 功能类似的新兴工具可能抢占市场份额 |
| 15   | 技术整合          | 可以与其他软件或技术整合           | 功能更新滞后            |

### 结论

- **选择多维表格**：如果你需要高级的数据处理能力、自动化功能、以及与团队成员的紧密协作，并且你愿意投入时间来学习和适应，多维表格会是一个更好的选择。
- **选择普通在线表格**：如果你的需求较为基础，重视成本效益、易用性以及广泛的文件格式兼容性，或者你倾向于使用用户基础广泛、学习成本低的工具，普通在线表格可能更适合你。

### 另外我再补充一点

目前我使用飞书表格类产品，主要是用于影刀 RPA 抓取数据的存储使用。在影刀的指令库中，也有现成的链接指令。

但对于多维表格，无论是否在知识库中，都可以使用 URL 上的字符串直接连接（勾选或取消是否为知识库即可）。

而对于普通的在线表格，只可以直接使用 URL 字符串连接非知识库的表格，如果是在知识库中的表格，需要进一步处理获取到 `spreadsheet_token` 才可以连接。

![](http://img.xlg.life/images%2F2024%2F06%2F08%2F20240608150005-7c52def2dcac74d033dd3b91a14035d2.png)

而让人讨厌的是，飞书中 「我的文档库」，居然就是一种默认的知识库，导致前期踩了很多坑。

> **通过 URL 字符串获取 `spreadsheet_token` 的小贴士**
>
> 1. 进入 [飞书API调度台](https://open.feishu.cn/api-explorer?from=op_doc_tab)
> 2. 左下角选择 `获取知识空间节点信息` 的 API
> 3. 左上角获取 `tenant_access_token`Token，填入 `请求头` 内
> 4. 点击 `开始调试`
> 5. 获取到的 `"obj_token": "*",` 就是想要的 `spreadsheet_token`
>
> 以上是我写给自己的白话文版，详细可以查看 [参考链接](https://www.yingdao.com/community/detaildiscuss?id=5dcf0bea-8168-4e5b-a552-985a7d0f4503)