# Git—Issue测试用例使用规范
## 核心要点
* Issue是什么？
2. New Issue规范
3. Running Issue规范
4. Closed Issue规范

## 一、Issue是什么？
### （一）、概念
Issue 指的是一项待完成的工作，通常与系统的改进相关，中文可以译为"问题"或"事务" ，系统中明确规定下面三种类型

*	BUG：系统中隐藏着的一些未被发现的缺陷、问题、漏洞
*	Task：**实现产品的先决条件、需求中没有明确定义但必须要做。**  
例如：冷启动脚本；接口定义调整；代码风格；接口查询性能；垃圾数据清理；代码重构；后台数据库的存储方式，修改前端技术框架；采用新的组件等
*	Feature：新需求(在PRD中没有涉及的需求)      
例如： 1、增加一种排序方式；#366,#368, #359

### （二）、组成部分
*	Title
*	Description
*	Labels
*	Assignee
*	Due date
*	Milestone

### （三）、重要程度

1. 所有出现的问题都必须在Issue体现记录
2. 每个 Issue 应该包含该问题的所有信息和历史
3. 正在进行中的Issue能够让所有项目参与者实时看到有哪些任务待完成、时间点、责任人等，方便开展工作
4. 已经Close的Issue方便后来的人只看这个 Issue，就能了解问题的所有方面和过程。并且可以进行版本的追踪和统计

## 二、New Issue——>规范
### (一)	New Issue 书写规范
1.	**Title 标题**
 * 每个Issue必须能够从标题上明白是什么问题
 * PS:一句话说清问题，参考4W1H要素(Who在When在Where,how发生了What)，简明扼要的说明自己提出的问题
2.	**Description 描述**
 *	学会使用MacDown书写规范（具体的MarkDown格式见后面）
 *	在文本框内描述问题详情（必填），及相应解决方案（选填）
 *	写明解决方案的时候，必须加上相应的具体描述和流程图，角色-任务流程图、数据流程图等
 *	涉及到界面的问题必须要有图示说明，点击右下角的上传附件（attach a file）
 *	如果不能够彻底说清楚可以点击右下角的上传文件（attach a file）
 *	其它问题可选择写上对象ID（角色、人、offer)，接口，返回值...
 *	可以@指定的人
3.	**Labels：Issue 可以贴上标签，这样有利于分类管理和过滤查看**
 *	没有标签或者标签不足时候，点击创建新标签
 *	已有标签要选择以下三个类别
        1. Category-类别 : BUG  /  Task  /  Feature
        2. Priority-优先级 : Resolve Immediately  /  Normal Queue  /  Not Urgent
        3. Type-类型 : Back-End   /    Front-End

4.	**Assignee:负责人**   
   指定具体的负责人，由相应的负责人统筹该Issue的事情，定位问题以及后续的解决方案的记录（支持重新指定负责人）
5.	**Due date：到期时间（选填，后期可以变更）** 
6.	**Milestone**  
 选择问题解决的版本(只能是上线版本，选择正确的版本；后期可以变更)


###  (二)	MarkDown格式
*主要介绍一些常用的MarkDown格式，具体的请查看链接：http://www.markdown.cn*

1.	标题，在行首插入1->6个#，对应1到6级标题
2.	换行，在末端书写两个空格，按回车
3.	一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行
4.	引用，在每一行的最前端加上 “>”(可以嵌套使用)
5.	列表分为无序列表和有序列表。无序列表使用星号、加号或是减号作为列表标记，有序列表则使用数字加一个英文句号
6.	分割线，在一行中使用三个以上的星号、减号和底线来建立一个分割线
7.	强调：使用星号（*）和底线（_）作为标记强调字词的符号，被 * 或 _ 包围的字词会被转换成斜体，用两个 * 或 _ 包起来的话，则会被加粗
8.	图片：点击右下角的Attach a file  
9.    所有的英文单词，在两侧加上"`  `"符号，以来区分英文与中文，增强可读性，例如： `order`

## 三、Running Issue——>规范 
### （一）、添加comment
1.	打开Issue
2.	在在输入框内添加comment，并且可以@相关人员
3.	写明解决方案的时候，必须加上相应的具体描述和流程图，角色-任务流程图、数据流程图等


**备注：在issue中Comment中必须有清晰的解决路径**

    1. 已确认；@Author
    2. 已修正，待部署测试 @linlin.liu
    3. 已测试，待部署上线 


### （二）、EditIssue
1.	打开Issue
2.	点击上方的Edit，对Issue进行重新编辑，以上所有的组成部分均可以修改：Title、Description、Labels、Assignee、Due date、Milestone，并且可以修改对应的project
3.	修改完成之后，点击submit，提交即可，可以在Issue的历史记录中查看到相应的操作记录

## 四、Closed Issue——>规范
1.	谁开启谁关闭原则：issue原则上只能由Author来Close
2.	所有关闭的Issue必须得到了解决，并且由解决人、测试人标记清楚输出最终结果
2.Millstone，移到下一个Millstone必须足够的理由
