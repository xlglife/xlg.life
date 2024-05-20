---
{"dg-publish":true,"permalink":"/5-主题/@第二优先级/Obsidian/Obsidian 插件 Templater/","tags":["Obsidian/插件"],"noteIcon":"1","created":"2023-09-19","updated":"2024-04-10"}
---

简介:: 模板增强插件

## 教程
- [在Obsidian中构建高效笔记模板，从Templates到Templater！\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1c64y1W7c2/)
## 语句
### tp.file
- 文件标题 `<% tp.file.title %>`
- 创建时间 `<% tp.file.creation_date() %>`
### tp.date
- 今天 `<% tp.date.now("YYYY-MM-DD") %>`
- 明天 `<% tp.date.now("YYYY-MM-DD", 1) %>`
- 明天 `<% tp.date.tomorrow("YYYY-MM-DD") %>`
- 昨天 `<% tp.date.now("YYYY-MM-DD", -1) %>`
- 昨天 `<% tp.date.yesterday("YYYY-MM-DD") %>`
### tp.system
- 提示输入 `<% tp.system.prompt("请输入内容") %>`
- 选择输入 `<% tp.system.suggester(["待办","进行中","完成"],["待办","进行中","完成"],true,"提示内容") %>`

## 代码片段

> [!note]- 在文章正文中添加天气信息
> 来源：[【搭建你的日记本】在文章正文中添加天气信息 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/19067)
> ```
> <%* 
> let url = 'https://www.tianqi.com/beijing/' 
> let res = await request({url: url,method: "GET"}); res = res.replace(/\n/g,'')
> let dqwd = /<p class="now"><b>(\d+)<\/b><i>℃<\/i><\/p>/.exec(res) 
> let tqwdfw = /<span><b>(.*?)<\/b>(.*?)<\/span>/.exec(res) 
> let sdfxzwx = /<dd class="shidu"><b>(.*?)<\/b><b>(.*?)<\/b><b>(.*?)<\/b><\/dd>/.exec(res) 
> let kqzlrcrl = /<dd class="kongqi" ><h5 style="background-color:#[0-9a-z]{6};">(.*?)<\/h5><h6>(.*?)<\/h6><span>(.*?)<br \/>(.*?)<\/span><\/dd>/.exec(res) 
> let 当前温度 = '当前温度：' + dqwd[1]+'℃' 
> let 天气 = '天气：' + tqwdfw[1] 
> let 温度范围 = '温度范围：' + tqwdfw[2] 
> let 湿度 = sdfxzwx[1] 
> let 风向 = sdfxzwx[2] 
> let 紫外线 = sdfxzwx[3] 
> let 空气质量 = kqzlrcrl[1] + ' ' + kqzlrcrl[2] 
> let 日出日落 = kqzlrcrl[3] + ' ' +kqzlrcrl[4] 
> -%>
> <% 当前温度 %> 
> <% 天气 %> 
> <% 温度范围 %>
> <% 湿度 %> 
> <% 风向 %>
> <% 紫外线 %>
> <% 空气质量 %> 
> <% 日出日落 %>
> ```

> [!note]- 选择样式插入 Callouts
> 来源：[obsidian templater终极指南 ｜ 轻松记笔记的技巧\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1qu411c7B5/)
> ```
> <%*
> const callouts = {
> note: '🔵 ✏ Note',
> info: '🔵 ℹ Info',
> todo: '🔵 🔳 Todo',
> tip: '🌐 🔥 Tip / Hint / Important',
> abstract: '🌐 📋 Abstract / Summary / TLDR',
> question: '🟡 ❓ Question / Help / FAQ',
> quote: '🔘 💬 Quote / Cite',
> example: '🟣 📑 Example',
> success: '🟢 ✔ Success / Check / Done',
> warning: '🟠 ⚠ Warning / Caution / Attention',
> failure: '🔴 ❌ Failure / Fail / Missing',
> danger: '🔴 ⚡ Danger / Error',
> bug: '🔴 🐞 Bug',
> };
> 
> const type = await tp.system.suggester(Object.values(callouts), Object.keys(callouts), true, '选择 callout 类型');
> const fold = await tp.system.suggester(['无', '展开', '折叠'], ['', '+', '-'], true, '选择 callout 折叠选项');
> 
> const title = await tp.system.prompt('标题:', '', true);
> let content = await tp.system.prompt('内容 (Shift + Enter 换行):', '', true, true);
> content = content.split('\n').map(line => `> ${line}`).join('\n')  
> 
> const calloutHead = `> [!${type}]${fold} ${title}\n`;
> 
> tR += calloutHead + content
> -%>
> ```