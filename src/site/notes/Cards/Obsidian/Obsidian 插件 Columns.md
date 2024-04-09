---
{"dg-publish":true,"permalink":"/Cards/Obsidian/Obsidian 插件 Columns/","tags":["Obsidian/插件"],"noteIcon":"👀 关注","created":"2023-12-25","updated":"2023-12-31"}
---

## 教程
- [Obsidian 插件：Obsidian Columns 支持分栏书写美化你的笔记样式](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-columns/)
- [[Obs＃84] 另一个更简便的笔记多栏作法：使用Columns插件\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1wT4y1k7SV/)
- [GitHub - tnichols217/obsidian-columns](https://github.com/tnichols217/obsidian-columns)
## 说明
- 插件设置保持默认即可
- 安装插件后，有三种语法格式可以进行分栏，分别是

| 格式 | 实时预览 | 设置选项 | 参考语法 |
| --- | --- | --- | --- |
| 标注 Callout | 支持 | 较少 | [[Cards/Obsidian/Obsidian 插件 Columns#标注 Callout 格式\|Obsidian 插件 Columns#标注 Callout 格式]] |
| 代码块 Codeblock | 支持 | 完整 | [[Cards/Obsidian/Obsidian 插件 Columns#代码块 Codeblock 格式\|Obsidian 插件 Columns#代码块 Codeblock 格式]] |
| 列表 List | 不支持 | 较少 | [[Cards/Obsidian/Obsidian 插件 Columns#列表 List 格式\|Obsidian 插件 Columns#列表 List 格式]] |


## 参考语法

### 标注 Callout 格式
#### 基础用法
> [!col]
> 第一栏
>
> 第二栏

#### 栏位内换行
> [!col]
> 第一栏
> 
>> [!col-md]
>> 第二栏
>> 
>> 第二栏多行

#### 调整栏位宽度
> [!col]
> 第一栏
>> [!col-md-3]
>> 第二栏
>> 
>> 这一栏宽度是第一栏的三倍

### 代码块 Codeblock 格式

#### 基础用法
````col
```col-md
第一栏
```
```col-md
第二栏
```
````

#### 为整体添加设置选项
[语法说明](https://github.com/tnichols217/obsidian-columns?tab=readme-ov-file#codeblock-settings-block)
````col
textAlign=right
===
```col-md
第一栏
```
```col-md
第二栏
```
````
#### 为栏位添加设置选项
[语法说明](https://github.com/tnichols217/obsidian-columns?tab=readme-ov-file#codeblock-settings-block)
````col
```col-md
textAlign=right
===
第一栏
```
```col-md
flexGrow=3
===
第二栏
```
````
### 标注 & 代码块 组合复杂示例
```````col
``````col-md
flexGrow=1
===
> [!info] Callouts
>  Stuff inside the callout
>  More stuff inside.
>> [!ERROR] Error description
>>  Nested callout
>>  `````col-md
>>  - example MD code
>>  - more stuff
>>  `````
``````

``````col-md
flexGrow=2.5
===
# Text annotation example:

`````col
````col-md
flexGrow=1
===
1. Function name **a** should be more descriptive

2. Remove **if/else** by using **||**
````

````col-md
flexGrow=2
===
```js
function a(word) {
	if (word != null) {
		console.log(word);
	} else {
		console.log("a");
	}
}
let msg = "Hello, world!";
console.log(msg)
```
````
`````
``````
```````

### 列表 List 格式

#### 基础用法
> 示例中的 `1`、`2` 是栏位宽度设置
- !!!col
    - 1
        - 第一栏
    - 2
        - 第二栏

#### 栏位内嵌套
- !!!col
	- 1
		# 栏位 1
		Some example text in column 1
		- some lists inside as well
			- more list items
	- 2
		# 栏位 2
		This column is twice as wide because it has the value set to 2
		- !!!col
			- 1
			  ## 栏位 2-1
			  You can even have columns inside columns!
			- 1
			  ## 栏位 2-2
			  More example text inside this column

---