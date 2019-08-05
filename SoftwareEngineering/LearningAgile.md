#执行合一：实现价值驱动的敏捷和精益开发
##Value Driven Agile and Lean Software Development

###前言
在不理解CMMI模型实践希望解决的问题的前提下，进行评估驱动的CMMI导入
使得过程改进对组织的质量文化起了负面作用

通过敏捷和精益实践，用==低成本==实现软件产品的==高价值==点

##第一部分 神形兼备的敏捷开发模式
###第一章：从先知后行到知行合一
==质量成本==是软件项目的杀手
==需求蔓延==是软件开发中的常见风险
####1.1 项目成功的标准
传统项目管理铁三角：需求范围，成本，进度；==没有关注项目要获取的价值，沉迷于需求，片面追求按时交付==
超多60%功能无用
初期无明确需求；面对不确定，计划可能不靠谱
价值的判断需要用户的使用反馈

敏捷铁三角 Jim Highsmith：
* 价值目标：可发布
* 质量目标：可靠，易更改
* 约束目标：特定约束下实现价值目标和质量目标

新的项目管理铁三角：
* 价值+能力目标：价值站在组织角度，人的能力提升
* 质量目标：不仅是功能正确，管理技术负债，可维护
* 约束目标：进度和成本

==在特定约束条件下，控制产品遗留隐患对交付产品的使用及维护的影响，关注人员能力提升，尽可能将项目/产品价值最大化==
以投资回报分析作为管理者的决策方式
####1.2 瀑布模式为代表的传统开发方法
瀑布模式只适用于简单项目
没有必要的反馈，以保证及时发现问题，及时调整，问题会被传递下去；信息流失
很少有团队执行100%瀑布模式，即设计在需求完成前就开始了
实际中，需求会变，人员会变，技术方案会变；但瀑布模式惩罚变更
在项目前期，对产品理解最差时识别出产品的需求范围
不能支持跨职能团队的磨合
####1.3 复杂项目共性：需求的不确定和技术的不确定
需求的进化：需求自然进化和需求失控蔓延
需求蔓延：客户和开发团队缺乏沟通，客户随意加需求，不做价值分析，不考虑实施成本；开发随意假设用户意图追加需求
==每条需求都是成本，但不是每条需求都有价值==
团队一开始不了解自己的开发效率；跨职能团队磨合
####1.4 从先知后行到知行合一
敏捷是人类自然做事的方式
敏捷开发的4个核心元素：
* 迭代开发
* 特性驱动：从任务分解结构管理转向特性分解结构管理
* 时间盒：固定时间完成一个活动；先有后优
* 增量提交

==敏捷就是在开发中学习，成长，调整和完善==
快速反馈，不断审查然后调整,降低错误成本，加深对产品的理解和对团队能力的理解

任务驱动：把关注点从实现的产品需求功能特性移开；进度压力前，减少任务，首先压缩质量控制相关的活动，如技术评审，测试，牺牲质量为代价
敏捷开发模式的两个主要特征：迭代开发；需求特性驱动管理（进度压力前，不会牺牲质量，而是减少用户特性）
### 第二章： 敏捷开发，摸着石头过河的智慧
####2.1 敏捷宣言和敏捷原则
**敏捷宣言**
* 个体和互动 高于 流程和工具
* 工作的软件 高于 详尽的文档
* 客户合作 高于 合同谈判
* 响应变化 高于 遵循计划

在传统开发模式下，==盲目强调过程符合==的文化下，这些价值观没有真正得到体现
敏捷宣言是方向性的东西，不能完全忽略右项

**敏捷12条原则**
1. 尽早，持续交付有价值的软件是我们满足客户的最优先考虑
2. 即使到了开发后期，也欢迎需求变更。敏捷过程利用变更为客户创造竞争优势
3. 频繁交付可以工作的软件，交付时间越短越好，可以从一周到一两个月
4. 在整个项目开发期间，业务人员和开发人员必须可以天天随时沟通，一起解决问题
5. 围绕一群有动力的个人进行项目开发。给他们提供所需要的环境和支持，并且相信他们会把事情做好
6. 对一个开发团队来说，面对面沟通是最高效的传递信息的方法
7. 工作的软件是软件开发中首要进展度量指标
8. 敏捷过程提倡可持续的开发。产品的赞助者，开发者和用户应该能够保持一个长期的，恒定的开发节奏
9. 不断关注卓越技术及优秀设计能增强敏捷力
10. 简于形，是最大地减少不必要工作的艺术，这是敏捷的精髓
11. 自我组织的开发团队能够逐步摸索出最适合的构架，需求和设计
12. 每隔一定时间，团队会在如何才能更有效地工作方面进行反省，然后对自己的做事方式进行必要调整

####2.2 敏捷开发架构与Scrum：调整中增量开发
敏捷管理活动以Scrum为核心，工程活动以极限编成方法为主，但不局限
**敏捷开发架构** by Highsmith
1. 产品愿景阶段
项目目标及约束（做什么）
团队相关成员（谁来做）
协同工作方式（如何做）
2. 推测阶段
==围绕需求特性建立产品发布计划==，包括：
收集分析初始需求
估计开发成本信息
考虑风险缓解策略
制定开发计划
3. 探索阶段
提交规划的需求特征子集
协作，自我组织
沟通，加深对产品价值及约束条件的理解
4. 调整阶段
评审迭代完成的需求功能特性，对产品需求做出调整
调整迭代计划和发布计划
5. 关闭阶段
项目结束点，也是总结点

推测，探索，调整闭环，替代了瀑布开发中的计划，执行，纠错

Scrum对应复杂场景，不确定性，不可预测性，定义过程不适用
定义的过程：可重复的生产过程，可预测
实验的过程：复杂产品；透明，审查，调整

**Scrum概述**
* 产品经理 Product Owner：维护优先级排列的产品需求列表 product backlog
* 在迭代sprint计划时，团队从product backlog中选取一部分，放入迭代需求列表 sprint backlog，并决定如何开发这些需求功能能
* 在固定周期完成一个迭代，通常是2-4周，团队每天会一起评估项目进展daily scrum
* 在上述过程中，Scrum过程经理 Scrum Master 让团队关注迭代目标的实现，并遵循Scrum实践
* 每次迭代结束，团队代码是可提交的，可直接让用户使用，或展示给客户
* 迭代最后两个活动：迭代评审sprint review和迭代回顾retrospective；根据反馈对产品和过程做优化调整
* 下轮迭代开始前，Scrum团队Scrum team从product backlog中选取一部分放入 sprint backlog，开始下一轮迭代

**3个角色**
* 产品经理 Product Owner
* Scrum过程经理 Scrum Master
不是真正的经理，和团队之间不是管理和被管理的关系；更像是过程教练
* Scrum团队 Scrum Team
5-9人的跨职能团队
具备需求分析，设计，编码，测试，技术资料编写等软件开发的全部技能
**3个文档**
* 产品需求列表 Product Backlog
用用户故事来表示每一个需求项，==产品经理==将他们按价值排序
用户故事颗粒度遵循==近细远粗==：排在上面的细化，以支持近期迭代的实施，底层故事颗粒度可以很大，因为后续可能更改，或不需要
* 迭代需求列表 Sprint Backlog
==由团队负责管理==，定义了Scrum团队某次迭代承诺实现的用户故事或任务，每次迭代应有主题
* 燃尽图 Burn Down Chart
监控版本及迭代开发进展
    * 版本燃尽图：==本次版本中==未开发的需求项或剩余的工作
    * 迭代燃尽图：==一次迭代中==未完成的工作

**5个会议**
* 产品需求列表的细化会议：细化列在前面的用户故事，为近几次迭代做准备
* 迭代计划会议：形成迭代需求列表
* 每日站立会：让团队成员工作同步，同时及时识别并解决任何影响实现迭代目标的障碍
* 迭代评审会议：演示完成的需求功能，让产品经理，客户及其他利益相关人加深对产品的理解，调整产品需求列表
* 迭代回顾会议：对迭代中的问题及好的做简单的根因分析，如有必要，调整scrum过程及实现

####2.3 Scrum是一个实现敏捷价值及原则的开发管理架构

### 第三章： 形神兼具，实现敏捷的核心价值
随意选择部分实践而忽略其他关联活动不会将Scrum的价值潜力真正发挥出来
敏捷只在团队层面实施，而整个公司的文化，理念和敏捷格格不入
形似而神不似

极限编程可以有效地支持Scrum的执行
####3.1 形似而神不似的Scrum实施
**Scrum不能保证解决问题，而能保证暴露问题**
同时做多件事是效率的杀手
需求分层细化，需求优先级才会起到作用
习惯了被动接受任务，主动就成为陌生词
一个不容易实现的实践往往是一个对组织价值大的实践
**没有本地化适配，敏捷过程很难落地生根**
==增量实施，先易后难==
**不要因为错误的原因引入Scrum，要明确引入敏捷的目的**
不少管理者不理解为何要引入敏捷
要对自己的开发过程的瓶颈做个诊断，做根因分析
####3.2 使用Scrum的艺术
决定成败的要点：
**Scrum中的自我管理及实现方式**

####3.3 极限编程是Scrum最好的伙伴
eXtreme Programming， XP
**技术负债：Scrum的杀手**
片面追求技术捷径，长期积累拖垮团队
**极限编成的4个核心价值**：沟通，简洁，反馈，勇气
**极限编程的原则**
**5个基本原则**

**10条一般原则**
* 鼓励授人以渔 teach learning
* 控制前期投入 small initial investment
* 坚信战则能胜 play to win
* 决策试验验证 concrete experiments
* 坦诚沟通文化 open，honest communication
* 做事尊重人性 work with people's instincts, not against them
* 敢于但当责任 accepted responsbility
* 结合本地特点 local adaption
* 团队轻装上阵 travel light
* 真实客观度量 honest measurement


##第二部分 建立以Scrum为框架的软件开发管理体系



#
==**CPM**==： Critical Path Methods
**Gantt Chart**
**WBS**: Work Breakdown Structures
**Project Constraints** 
project management is considered a combination of art and science
tasks on the critical path
**Project Resource Planning**: Loading resources into the project schedule equips the Gantt chart with reality
**Project Control**
project management triangle: ==Time, Cost and Quality==
to find the optimum point where all these three intersect
resource leveling: move the task within its allowable time window
==**CPD**==: Collaborative Product Development
Phases comprised of activities and deliverables and gates are for the executive managers to decide whether to allow the project to move on, postponed, reduced in scope, or canceled

==a general CPD process==:
**Phase One (Concept Development)**
• Tasks:
Defining Customer Requirements
Developing Proof of Concept
Intellectual Property Study
Developing Product Quality Metrics
• Deliverables:
Marketing Requirement Specifications
Concept Prototypes
IP Report
Marketing Test Specifications
**Gate One**
**Phase Two (Project/Product Planning and Architecture)**
• Tasks:
Project Planning Including Development, Manufacturing,
Regulatory, and Quality/Reliability Planning
Developing Product Architectural Plan included with the
functional modules and components and also Risk Management
Study
• Deliverables:
All Project, Manufacturing, and Regulatory Plans and Risk
Assessments
All Architectural Documents including Modules and Component
Requirements and Test Specs

**DFM**: design for manufacturing
* Reduce the total number of parts
* Develop a modular design
* Use of standard components
* Design parts to be multifunctional
* Design parts for multiuse(in different products)
* Design for ease of fabrication
* Design with standard interfaces
* Maximize compliance by following one standard process, tool, and method from design to manufacturing