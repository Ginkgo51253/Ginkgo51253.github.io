---
title: "First Unity Demo"
permalink: "/FirstUnityDemo/"
---

Return to [Home page](https://Ginkgo51253.github.io/Home)

---

# 记录自己第一个unity的Demo建立过程

![UnityDemo01](https://github.com/Ginkgo51253/Ginkgo51253.github.io/blob/master/Pictures/FirstUnityDemo01.PNG?raw=true)

<i>所有资源与代码存放在[我的Git仓库](https://github.com/Ginkgo51253/GK_storage/blob/master/新手勇者与二段跳.zip)中，如有必要可以随意下载查看</i>

## 1. 选题

Unity是我刚刚接触没多久的一款游戏引擎，鉴于操作的熟练程度有限，游戏的制作过程中需要多次翻阅UnityAPI手册与查阅网上的相关信息来逐步实现游戏功能。因此需要选择一个相对简单的游戏入手进行制作。

《新手勇者与二段跳》是《战斗天赋解析系统》的内置小游戏，操作方法只有点击，控制玩家角色跳起以躲避障碍。游戏目标为获得更高的得分，随着玩家游玩时间的增长与碰触敌人，玩家的得分会随之增长。游戏控制方法简单，模型数量少，构造简单，适合于建立一个简单的快速模型。  

综上，我并没有选择去自己设计一款新的小型游戏，而是选择仿制一款已经存在的简单游戏进行Demo的制作。

## 2. 功能点分析

1. 地面、阻挡物的构建与刷新机制
2. 玩家控制方式与自动行为
3. 敌人的构建与刷新机制
4. 游戏得分的显示
5. unity进行的功能整合

## 3. 详细实现过程

### 1. 地面与阻挡物构建

地面与阻挡物使用同一个游戏对象（板块）进行构建，每个板块在unity中设定好长宽后，添加多个空对象存放这些板块，通过设置```gameObject.transform.position```将板块摆放为地面、阻挡物（下图为地面的摆放方式）

![UnityDemo02](https://github.com/Ginkgo51253/Ginkgo51253.github.io/blob/master/Pictures/FirstUnityDemo02.PNG?raw=true)

摆放好后，为地面、阻挡物的父对象添加一个碰撞箱用来表示碰撞范围，最终将阻挡物拖入资源文件夹中存为预制（Prefab），供之后在代码中调用（下图为存放好的预制）

![UnityDemo03](https://github.com/Ginkgo51253/Ginkgo51253.github.io/blob/master/Pictures/FirstUnityDemo03.PNG?raw=true)

### 2. 添加玩家

第一步，添加玩家对象，玩家有多种状态需要多张不同的玩家图片来进行表示，制作玩家的图片集（如下图）

![UnityDemo03](https://github.com/Ginkgo51253/Ginkgo51253.github.io/blob/master/Pictures/FirstUnityDemo05.PNG?raw=true)

第二步，添加玩家自动行动的脚本，以玩家初始状态为基准，当玩家位置位于初始状态左侧时，赋予一个向右的速度控制玩家向右移动，当玩家碰撞到阻挡物时则无法向右移动，具体代码存放在Script/Main/PlayerAutoMove中。

第三步，添加玩家控制脚本，玩家着地时可以进行起跳操作，当玩家第一次起跳且在空中时，可以进行二段跳操作，这之后不再能继续跳跃，直到玩家落在平面上时才能重新起跳，具体代码在Script/Main/PlayerDoubleJump

第四步，添加玩家动画（虽然在这个Demo中玩家各个状态我只画了一帧），为玩家添加animator对象，创建无状态、跳跃、击杀敌人三个动画片段（animation clips），在animator中设置动画状态转化图，并设置变量对这些状态转化图进行控制，在Script/Main/PlayerDoubleJump中根据玩家状态修改animator的变量状态达到动画效果。

### 3. 添加敌人

第一步，添加敌人对象，敌人需要有多种样式，因此先制作几种不同的敌人对象（如下图）

![UnityDemo04](https://github.com/Ginkgo51253/Ginkgo51253.github.io/blob/master/Pictures/FirstUnityDemo04.PNG?raw=true)

第二步，为敌人添加碰撞箱，设置为触发器，添加脚本，具体代码在Script/Main/EnemyAction

第三步，将制作好的敌人拖入资源文件夹变为预制，为脚本调用。

### 4. 设置刷新逻辑

第一步，设计对象池存储结构，用哈希表存储一系列链表，链表中存放各个类别的对象，当需要生成一个对象时，先在哈希表中查找这个类别，尝试从链表中获取，如果无法获取，则尝试从资源文件中获取。当使用完毕时，将不需要的对象分类别存放回哈希表中，以此实现对象池的功能。

第二步，设计显示时对象存储结构，用链表存储一系列对象，依次访问和修改相应参数，当需要生成新对象时尝试向哈希表发出请求，当对象需要被回收时将对象放回哈希表中。

第三步，将上述功能整合，同时适用于敌人的生成和阻挡物的生成，其中存储结构可以共用，抽象为一个单独的脚本对象，具体代码为Script/Main/BlockObject，而生成器分化为阻挡物和敌人两种类型，具体代码分别为Script/Main/BlockerGenerator和Script/Main/EnemyGenerator

---

Return to [Home page](https://Ginkgo51253.github.io/Home)