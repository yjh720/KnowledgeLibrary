[敏捷开发流程之Scrum：3个角色、5个会议、12原则 - 大码哥 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xichji/p/12164740.html)

# 5个会议
## 待办事项整理会议（Backlog Grooming Meeting）
参会成员：Product Owner，Scrum Master，关键开发者，架构师，Optional Team Leader（硬件，机械臂算法，视觉算法，电气）

时间：代计划会议开始之前3天

时长控制：30-60min

会议内容：
由Product Owner将一批希望团队在下次迭代时实现的用户故事，按照**实现顺序**描述给在场的团队成员，Scrum Master与在场成员分析用户故事，明确指出团队认为需求不明确的地方，Product Owner现场记录，会后补全，Scrum Master与架构师，还有在场成员分析用户故事需要包含哪些技术任务，Scrum Master和关键开发者，架构师讨论建立下一轮Sprint子任务，方便迭代计划会议的时候团队可以更准确地预估任务故事点。

预备材料：
	Product Backlog：对应飞书文档需求表，Product Owner->Product Backlog->用户故事（需求），优先级，~~验收标准(optioal)~~

内容产出：
	Product Backlog：对应飞书文档需求表，Product Owner->经过讨论的用户故事（需求）
	Sprint Backlog：对应飞书文档任务表，Scrum Master->子任务(不包含时间，人员分配，实现方法)

## 迭代计划会议（Sprint Planning Meeting）
参会成员：Product Owner，Scrum Master，Team（程序员、测试员、用户体验设计）

时间：迭代开始第一日

时长控制：60-120min

会议内容：
选择本次迭代的Backlog和估算本次迭代的工作量。
产品负责人逐条讲解最重要的产品功能，开发团队共同估算Backlog所需工作量，直到本迭代工作量达到饱和。产品负责人参与讨论并回答和需求相关的问题，但不干扰估算结果。队员认领任务（或由组长协商分发），独立或与别人一起完成任务（what），队员讨论实现方法（how），确认每项任务所需时长。

预备材料：
	Product Backlog：对应飞书文档需求表，Product Owner->经过讨论的用户故事（需求）
	Sprint Backlog：对应飞书文档任务表，Scrum Master->子任务(不包含时间，人员分配，实现方法)

内容产出：
	Sprint Backlog：对应飞书文档任务表，Scrum Master->子任务(包含时间，人员分配，实现方法)

## 每日站会（Standup Meeting）
参会成员：Team（程序员、测试员、用户体验设计）

时间：每天工作之前

时长控制：15min

会议内容：
团队内部利用每日立会来沟通进度，开发团队利用燃尽图来展示整体进度；如无特殊原因，迭代期内无变更，在每日站会上团队成员需要回答以下3个问题：
-   昨天你做了什么?
-   今天你将要做什么?
-   你有需要帮助的地方吗?

## 评审会（Review Meeting）
参会成员：Product Owner，Scrum Master，Team（程序员、测试员、用户体验设计），可能还有客户

时间：一轮Sprint结束

时长控制：60-120min

会议内容：
小组向产品负责人展示迭代工作结果，产品负责人给出评价和反馈。以用户故事是否能成功交付来评价任务完成情况。

## 反思会（Retrospective Meeting）
参会成员：Product Owner，Scrum Master，Team（程序员、测试员、用户体验设计）

时间：一轮Sprint结束

时长控制：15-30min

会议内容：在每个迭代后召开简短的反思会，总结哪些事情做得好，哪些事情做得不好。做得好的保留，不好的摒弃。会议得出这样的结论：开始做什么、继续做什么、停止做什么。