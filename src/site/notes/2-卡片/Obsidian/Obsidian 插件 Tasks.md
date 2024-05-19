---
{"dg-publish":true,"permalink":"/2-卡片/Obsidian/Obsidian 插件 Tasks/","tags":["Obsidian/插件"],"noteIcon":"1","created":"2024-05-09","updated":"2024-05-09"}
---

简介:: 任务管理插件

## 常用查询语法
1. 完成/未完成：`done` 或 `not done`
2. 完成日期：`done before/after/on 日期`
3. 无到期日：`no due date`
4. 截止日期：`due before/after/on 日期`
5. 日期可使用 `today, yesterday, tomorrow, next week, last Friday, in two weeks` 等
6. 路径
	- 要搜寻：`path includes 路径`
	- 不搜寻：`path does not include 路径`
7. 事项描述
	- `description includes 字串`
	- `description does not include 字串`
8. 最靠近标题
	- `heading includes 标题`
	- `heading does not include 标题`
9. 是否重复
	- `is recurring`
	- `is not recurring`
10. 排除某个事项：`excludes 清单事项`
11. 限制显示事项数目：`limit to 数值 tasks`
12. 排序：`sort by (status|due|done|path|description)`
13. 显示样式隐藏 
	- `hide edit button` 隐藏编辑按钮
	- `hide backlink` 隐藏反向链接
	- `hide done date` 隐藏完成日期
	- `hide due date` 隐藏截止日期
	- `hide recurrence rule` 隐藏重复规则
	- `hide task count` 隐藏任务数量统计

## 参考示例
#### 复刻插件侧边栏 Tasks Calendar Wrapper
````
## 待办事项
```tasks
not done
due on or after today
group by due
```
## 已过期
```tasks
not done 
due before today
group by backlink
```
## 未安排
```tasks
not done
no due date
group by backlink
```
````

#### 最近完成的任务
````
```tasks
done
hide edit button
hide postpone button
sort by done reverse
hide task count
status.type is DONE
limit 10
```
````

#### 按文件夹分组的全部未完成任务
````
```tasks
not done
group by folder
```
````

## 参考链接
- [官方文档](https://publish.obsidian.md/tasks/Introduction)
- [Tasks插件专题 | obsidian文档咖啡豆版](https://coffeetea.top/zh/tasks/#_1-%E4%B8%93%E6%A0%8F%E4%BB%8B%E7%BB%8D)
- [Obsidian 插件：Tasks 更方便的任务管理 | Pkmer](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-tasks-plugin/)