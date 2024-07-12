# Cell-Intrusion-
A game. Your goal is to create a virus to attack the cell. Cells and viruses are composed of various building blocks, such as membranes, ion pumps, various workshops, nucleoids, etc.

# 基本介绍
## 简介
这应当被归属于策略游戏。玩家设计一个病毒，试图入侵和征服越来越复杂的细胞结构。病毒会尝试进入细胞、自我复制。从基本细胞（比如大肠杆菌）开始，随着关卡的提升，玩家将面对越来越棘手的关卡，比如呼吸道上皮细胞、肝细胞、生殖细胞、包含白细胞的多细胞系统、等等。玩家可以构建RNA病毒、DNA病毒、逆转录病毒，朊病毒，单层膜、双层膜病毒等等。关卡可能包含诸如”第一课：大肠杆菌”，“叶子”，“冷静的艾滋病”，“真正的挑战——呼吸道上皮细胞”，“最终局：一次感冒”，等等

## 游戏机制
细胞将由叶绿体、线粒体、ATP、离子泵、膜零件、拟核等组成。病毒将由复制开始码、转录开始码、增强子等构成，这些基本零件作为玩家设计病毒的零件库，玩家将像搭建乐高一样搭建病毒，搭建完成后病毒被释放到环境中。病毒会尝试进入细胞和自我复制。能否成功进入和自我复制的效率均取决于玩家的设计。
细胞和病毒由很多小组件构成。游戏后台会处理这些组件的相互作用。并没有被称为“细胞”和“病毒”的实体。

# 组件
## 基因表达
分成两个房间：蓝图转录车间和生产车间
### 蓝图转录车间
DNA作为一个固定的长链。DNA由几种不同类型的部分串联而成，这几个部分为：增强子、基因。**RNA聚合酶** 在转录车间中游走，直到碰到增强子，和DNA贴附，向前运动，直到碰到基因，状态改变为转录模式,产生一个实体，该实体IN:ATP,碱基 OUT: ADP, 状态进度条+1。状态进度条走满后产生RNA，RNA是一个rigidbody，存储卡形状，从洞口掉进生产车间。
转录车间的IN：ATP,ADP,碱基。 
ATP也在转录车间中碰撞。

### 生产车间
生产车间在蓝图转录车间的下面。生产车间里有几个核糖体，正好能接住上面掉下的RNA。核糖体接住RNA后，转化为运行态，显示自己要产生的蛋白。IN：氨基酸，ATP。 OUT：ADP，状态进度条+1。状态进度条走满后产生蛋白质，掉进机器分配线路，并且弹出RNA。
RNA是可复用的，一个核糖体弹出RNA后，RNA在生产车间碰撞，可能碰到下一个核糖体。
生产车间IN：中性、碱性、酸性氨基酸，ATP，ADP。

## 能量
葡萄糖转运进入细胞是被动转运，只需要转运蛋白。
ATP作为mikan里面的弹球。功能蛋白组件作为机器，弹球触碰到机器的进货口后被机器纳入，机器得到一定数量的弹球后产生反应物。
**葡糖糖转运蛋白**只长在发电机房和外界间的墙壁上。葡糖糖触碰到此蛋白（无论从内外），都会转运到墙壁对侧。
因此发电机房里面会聚集一些葡糖糖。
发电机房里面放置一些**葡萄糖ATP合成酶**，IN: 葡糖糖，6ADP， OUT：6ATP.

## 储能
葡萄糖用于合成糖原。由于是被动转运，葡萄糖不合成糖原的话会很容易跑掉。
（发现每一个机制都要用心想怎么实现，唉，，）
**糖原合成酶**是可逆的，IN: ATP, 葡萄糖 OUT: 本身有一个糖原槽，就像尾巴一样长出来。ADP
当ATP和葡糖糖比较多时，自然会合成糖原，当ADP比较多时，自然会分解糖原。
糖原合成酶在发电机房里面。
## 物质

功能蛋白质是静态的，不会碰来碰去地运动（允许规则的运动）
还是mikan，DNA表达也可以使用Mikan的上游零件。随着游戏进程，逐渐解锁更多蛋白质。

## 摄入
一方面，可以用转运蛋白表示；
另一方面，用胞吞表示。胞吞可以表示为mikan里面的运货钩。这样也就可以胞吞病毒。

## 运输
采用一种“内部总线”的设计，参考cpu架构，factoria ，mikan的core 摧毁的小球轨道，也可以辅以多种专用线路。
内部总线运输常用分子，包括ATP、ADP。
“外部总线”也存在，作为血管，但这就很简单了。


#  概念（可能加入的设计）
## 能量机构 

​	能量产生器（太阳能板、叶绿素、天线分子），ATP分子。糖类分解器。 让光子是一个点大小，这样突出天线的作用。光子为平行光射入，这样突出叶绿素展开排布的作用。

​	能量存储器 糖类 糖类是链表形状，可以从任意节点断开，形成两个，也可以从末端分解，合成ATP。

​	任何其他机构的作用需要能量。

## 物质机构

​	氨基酸 大分子需要氨基酸，且能分解为氨基酸。来源：或者从外部摄入肽链，或者摄入氨基酸。

​	脂质单元 膜单元需要脂质

​	核酸单元。合成RNA和DNA需要核酸单元，从外部摄入片段或单元。

## 膜
略
​	
## 修复机构

​	DNA修复酶、蛋白质降解器。

​	修复或降解任何出问题的东西。所谓降解，就是把大分子变成小分子，或直接删除，以免占用空间。

## 蛋白质生产机构

​	核糖体

​	需要附着在RNA上，用ATP合成蛋白质。

## 核酸维护机构

​	DNA复制酶

​	RNA转录酶

## 次级生产机构

​	合成酶 太阳能板组装机 多糖组装器 轨道单元组装器 膜单元组装器

​	合成小分子。

## 运输机构

​	轨道交通、碰撞小球、分隔空间、电线、全局变量

​	轨道单元 运输车 收集器 筛选器 特化收集器 

​	膜单元

## 其他

​	压力板能量产生器 

----

# Basic Introduction
## Introduction
This should be classified as a strategy game. Players design a virus to try to invade and conquer increasingly complex cell structures. The virus will try to enter the cell and replicate itself. Starting from basic cells (such as E. coli), as the levels are upgraded, players will face increasingly difficult levels, such as respiratory epithelial cells, liver cells, germ cells, multicellular systems containing white blood cells, etc. Players can build RNA viruses, DNA viruses, retroviruses, prions, single-layer membrane, double-layer membrane viruses, etc. Levels may include such as "Lesson 1: E. coli", "Leaf", "Calm AIDS", "Real Challenge-Respiratory Epithelial Cells", "Final Game: A Cold", etc.

## Game Mechanics
Cells will be composed of chloroplasts, mitochondria, ATP, ion pumps, membrane parts, nucleoids, etc. Viruses will be composed of replication start codes, transcription start codes, enhancers, etc. These basic parts serve as the parts library for players to design viruses. Players will build viruses like building Lego, and after the construction is completed, the viruses will be released into the environment. Viruses will try to enter cells and replicate themselves. Whether it can successfully enter and the efficiency of self-replication depends on the player's design.
Cells and viruses are made up of many small components. The game background will handle the interaction of these components. There is no entity called "cell" and "virus".

# Components
## Gene expression
Divided into two rooms: blueprint transcription workshop and production workshop
### Blueprint transcription workshop
DNA is a fixed long chain. DNA is composed of several different types of parts in series, these parts are: enhancer, gene. **RNA polymerase** wanders in the transcription workshop until it encounters an enhancer, attaches to DNA, and moves forward until it encounters a gene. The state changes to transcription mode, and an entity is generated. The entity IN: ATP, base OUT: ADP, status progress bar +1. When the status progress bar is full, RNA is generated. RNA is a rigidbody, in the shape of a memory card, and falls into the production workshop from the hole.
Transcription workshop IN: ATP, ADP, base.
ATP also collides in the transcription workshop.

### Production workshop
The production workshop is below the blueprint transcription workshop. There are several ribosomes in the production workshop, which can just catch the RNA dropped from above. After the ribosome catches the RNA, it is converted to the running state and displays the protein it wants to produce. IN: amino acids, ATP. OUT: ADP, status progress bar +1. When the status progress bar is full, protein is produced, falls into the machine distribution line, and RNA is ejected.
RNA is reusable. After a ribosome ejects RNA, RNA collides in the production workshop and may touch the next ribosome.
Production workshop IN: neutral, alkaline, acidic amino acids, ATP, ADP.

## Energy
Glucose transport into cells is passive transport, which only requires transport proteins.
ATP is the pinball in mikan. The functional protein component is the machine. The pinball touches the machine's inlet and is taken in by the machine. The machine produces reactants after receiving a certain number of pinballs.
**Glucose transport protein** only grows on the wall between the generator room and the outside world. When glucose touches this protein (whether from inside or outside), it will be transported to the opposite side of the wall.
Therefore, some glucose will gather in the generator room.
Place some **Glucose ATP synthase** in the generator room, IN: glucose, 6ADP, OUT: 6ATP.

## Energy storage
Glucose is used to synthesize glycogen. Since it is a passive transport, glucose will easily escape if it does not synthesize glycogen.
(I found that I have to think carefully about how to implement each mechanism, alas,)
**Glycogen synthase** is reversible, IN: ATP, glucose OUT: It has a glycogen tank that grows out like a tail. ADP
When ATP and glucose are more, glycogen will naturally be synthesized, and when ADP is more, glycogen will naturally be decomposed.
Glycogen synthase is in the generator room.
## Substance

Functional proteins are static and will not move around (regular movement is allowed)
Still mikan, DNA expression can also use Mikan's upstream parts. As the game progresses, more proteins will be gradually unlocked.

## Intake
On the one hand, it can be represented by transport proteins;
On the other hand, it can be represented by endocytosis. Endocytosis can be represented as a cargo hook in mikan. This also allows the endocytosis of viruses.

## Transport
Use an "internal bus" design, refer to the CPU architecture, factoria, mikan's core destroyed ball track, and can also be supplemented with a variety of dedicated lines.
The internal bus transports common molecules, including ATP and ADP.
"External bus" also exists as a blood vessel, but this is very simple.

# Concept (possible design)
## Energy mechanism

​ Energy generator (solar panel, chlorophyll, antenna molecule), ATP molecule. Carbohydrate decomposer. Let the photon be a point size, so as to highlight the role of the antenna. The photon is parallel light, so as to highlight the role of chlorophyll in unfolding and arranging.

​ Energy storage carbohydrates carbohydrates are in the shape of a chain list, which can be disconnected from any node to form two, or decomposed from the end to synthesize ATP.

​ The role of any other mechanism requires energy.

## Material mechanism

​ Amino acids macromolecules need amino acids and can be decomposed into amino acids. Source: either take in peptide chains from the outside, or take in amino acids.

​ Lipid unit Membrane units require lipids

​ Nucleic acid unit. Nucleic acid units are needed to synthesize RNA and DNA, and fragments or units are taken in from the outside.

## Membrane
Omitted
​
## Repair mechanism

​ DNA repair enzymes, protein degraders.

​ Repair or degrade anything that has gone wrong. Degradation means turning large molecules into small molecules, or directly deleting them to avoid taking up space.

## Protein production mechanism

​ Ribosome

​ Need to attach to RNA and use ATP to synthesize proteins.

## Nucleic acid maintenance mechanism

​ DNA replicase

​ RNA transcriptase

## Secondary production mechanism

​ Synthetase Solar panel assembler Polysaccharide assembler Track unit assembler Membrane unit assembler

​ Synthesize small molecules.

## Transport mechanism

​ Rail transit, collision balls, space dividers, wires, global variables

​ Track unit Transport vehicle Collector Filter Specialized collector

​ Membrane unit

## Others

​ Pressure plate energy generator
