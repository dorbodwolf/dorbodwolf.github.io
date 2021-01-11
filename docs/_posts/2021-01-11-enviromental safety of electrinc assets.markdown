**Topic**

\

Fire risk of electric assets

\

输电廊道上的潜在环境风险（特别是火灾）管控

\

**Nested asset types**

\

**Level1[ ]{.Apple-converted-space}**

\

Land Use mask layer

\

**Level2**[ ]{.Apple-converted-space}

\

Power transmission corridor

\

**Level3**[ ]{.Apple-converted-space}

\

Power lines

\

Tower

\

trees

\

[Weather station]{.s1}

**![pastedGraphic.png](file:///pastedGraphic.png)**

\

\

\

\

\

\

\

**Title**

\

Environmental risk prevention of power transmission facilities

\

**Aims**

\

为电力单位的植被管理团队提供关于资产的计划、实践和报告的精确模型，来简化他们高成本和复杂的现场数据收集和检查工作。我们希望帮助电力设施维护团队优化工作流程并降低业务成本。

Provide the vegetation management team of the electricity agency with
accurate models of asset planning, practice and reporting to simplify
their high-cost and complex field data collection and inspection work.
We hope to help the power facility maintenance team optimize work
processes and reduce business costs.

\

电力单位无法通过例行的野外作业来预测哪些资产需要修护或清理。希望帮助他们根据周围环境评估周围环境的状况，特别是输电廊道上植被的空间特征，预测这些环境因子的变化，来感知对公用事业资产的威胁。[ ]{.s2}

The electricity agency cannot predict which assets need repairing or
cleaning through routine field operations. Hope to help them assess the
condition of the surrounding environment based on the surrounding
environment, especially the spatial characteristics of the vegetation on
the power transmission corridor, predict the changes of these
environmental factors, and perceive the threat to public utility
assets.[ ]{.Apple-converted-space}

 

为电力单位提供快速高效的数据收集和检查[、]{.s3}提升数据准确性和质量[、]{.s3}帮助他们实现有效的团队协调与协作。我们旨在通过分析挖掘空间数据，来帮助电力单位识别和预测环境危害例如野火，评估经济[损失]{.s3}。

To provide electricity agency with fast and efficient data collection
and inspection, improve data accuracy and quality, and help them achieve
effective team coordination and collaboration. We aim to analyze and
mining spatial data to help power companies identify and predict
environmental hazards such as wildfires and assess economic losses.

\

**Decisions**

\

1.  []{.s2}为了安全，廊道内房屋都要被拆迁，总共涉及多少栋房屋，总共需要赔偿多少钱？
2.  []{.s2}为了安全，廊道内的耕地都要被弃用，廊道内的耕地面积有多少，涉及的土地价值有多少？
3.  []{.s2}**距离故障输电塔**[**5**]{.s2}**公里内的居民区有多少个？**
4.  []{.s2}[**有多少条道路需要设置警示牌来注意高压危险？**]{.s4}
5.  []{.s2}[**输电廊道上需要砍掉的离输电线路太近的树木有多少颗？**]{.s4}
6.  []{.s2}输电廊道上哪些树木因为靠近输电线路而需要修剪？
7.  []{.s2}所有输电廊道[1]{.s2}公里缓冲区内的用地类型有哪些？用地面积占比最大的和最小的用地类型分别是什么？
8.  []{.s2}按照受树木干扰威胁程度对编号为[A001]{.s2}对输电线路上的所有输电塔排序，并给出前三个输电塔之间的距离？
9.  []{.s2}编号为[X003]{.s2}的输电廊道单位面积的输电塔个数是多少？单位长度的树木个数是多少？

\

\

\

\

**Pyramid**

\

![1\_\_\#\$!@%!\#\_\_pastedGraphic.png](file:///1__%23$!@%25!%23__pastedGraphic.png)

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

**ER diagram**

\

![2\_\_\#\$!@%!\#\_\_pastedGraphic.png](file:///2__%23$!@%25!%23__pastedGraphic.png)

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

**Tables**

\

\

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Col | *     | **T   | **Not | **U   | **Pr  | **Fo  | **Ch  | **E   |
| umn** | *Deta | ype** | null  | nique | imary | reign | eck** | xclus |
|       | ils** |       | c     | c     | key** | key** |       | ion** |
|       |       |       | ons** | ons** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | \     | in    | Y     | Y     | Y     | \     | \     | \     |
|       |       | teger |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| L     | Land  | v     | Y     | \     | \     | \     | \     | \     |
| UTYPE | use   | archa |       |       |       |       |       |       |
|       | t     | r(50) |       |       |       |       |       |       |
|       | ypes: |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | \     |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [ ]   |       |       |       |       |       |       |       |
|       | {.App |       |       |       |       |       |       |       |
|       | le-co |       |       |       |       |       |       |       |
|       | nvert |       |       |       |       |       |       |       |
|       | ed-sp |       |       |       |       |       |       |       |
|       | ace}f |       |       |       |       |       |       |       |
|       | orest |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [ ]   |       |       |       |       |       |       |       |
|       | {.App |       |       |       |       |       |       |       |
|       | le-co |       |       |       |       |       |       |       |
|       | nvert |       |       |       |       |       |       |       |
|       | ed-sp |       |       |       |       |       |       |       |
|       | ace}r |       |       |       |       |       |       |       |
|       | eside |       |       |       |       |       |       |       |
|       | ntial |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [     |       |       |       |       |       |       |       |
|       |  ]{.A |       |       |       |       |       |       |       |
|       | pple- |       |       |       |       |       |       |       |
|       | conve |       |       |       |       |       |       |       |
|       | rted- |       |       |       |       |       |       |       |
|       | space |       |       |       |       |       |       |       |
|       | }road |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [     |       |       |       |       |       |       |       |
|       | ]{.Ap |       |       |       |       |       |       |       |
|       | ple-c |       |       |       |       |       |       |       |
|       | onver |       |       |       |       |       |       |       |
|       | ted-s |       |       |       |       |       |       |       |
|       | pace} |       |       |       |       |       |       |       |
|       | facil |       |       |       |       |       |       |       |
|       | ities |       |       |       |       |       |       |       |
|       | far   |       |       |       |       |       |       |       |
|       | mland |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [     |       |       |       |       |       |       |       |
|       | ]{.Ap |       |       |       |       |       |       |       |
|       | ple-c |       |       |       |       |       |       |       |
|       | onver |       |       |       |       |       |       |       |
|       | ted-s |       |       |       |       |       |       |       |
|       | pace} |       |       |       |       |       |       |       |
|       | water |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | indus |       |       |       |       |       |       |       |
|       | trial |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| P     | How   | b     | \     | \     | \     | \     | \     | \     |
| EOPLE | many  | igint |       |       |       |       |       |       |
|       | p     |       |       |       |       |       |       |       |
|       | eople |       |       |       |       |       |       |       |
|       | in    |       |       |       |       |       |       |       |
|       | the   |       |       |       |       |       |       |       |
|       | block |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| HOUSE | How   | b     | \     | \     | \     | \     | \     | \     |
|       | many  | igint |       |       |       |       |       |       |
|       | house |       |       |       |       |       |       |       |
|       | in    |       |       |       |       |       |       |       |
|       | the   |       |       |       |       |       |       |       |
|       | block |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| geom  | Geo   | \     | \     | \     | \     | \     | \     | \     |
|       | metry |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

\

\

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Col | *     | **T   | **Not | **U   | **Pr  | **Fo  | **Ch  | **E   |
| umn** | *Deta | ype** | null  | nique | imary | reign | eck** | xclus |
|       | ils** |       | c     | c     | key** | key** |       | ion** |
|       |       |       | ons** | ons** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | \     | in    | Y     | Y     | Y     | \     | \     | \     |
|       |       | teger |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| geom  | Geo   | \     | \     | \     | \     | \     | \     | \     |
|       | metry |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| \     | \     | \     | \     | \     | \     | \     | \     | \     |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| \     | \     | \     | \     | \     | \     | \     | \     | \     |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

\

\

\

\

\

\

\

\

\

\

\

\

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Col | *     | **T   | **Not | **U   | **Pr  | **Fo  | **Ch  | **E   |
| umn** | *Deta | ype** | null  | nique | imary | reign | eck** | xclus |
|       | ils** |       | c     | c     | key** | key** |       | ion** |
|       |       |       | ons** | ons** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | \     | in    | Y     | Y     | Y     | \     | \     | \     |
|       |       | teger |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| TE    | te    | v     | Y     | \     | \     | \     | \     | \     |
| XTURE | xture | archa |       |       |       |       |       |       |
|       | of    | r(50) |       |       |       |       |       |       |
|       | elect |       |       |       |       |       |       |       |
|       | rical |       |       |       |       |       |       |       |
|       | wire  |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "A"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "B"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "C"   |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| LPAR  | Par   | in    | Y     | \     | \     | \     | \     | \     |
| ALLEL | allel | teger |       |       |       |       |       |       |
|       | lines |       |       |       |       |       |       |       |
|       | of a  |       |       |       |       |       |       |       |
|       | elect |       |       |       |       |       |       |       |
|       | rical |       |       |       |       |       |       |       |
|       | wire  |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| geom  | \     | \     | \     | \     | \     | \     | \     | \     |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

\

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Col | *     | **T   | **Not | **U   | **Pr  | **Fo  | **Ch  | **E   |
| umn** | *Deta | ype** | null  | nique | imary | reign | eck** | xclus |
|       | ils** |       | c     | c     | key** | key** |       | ion** |
|       |       |       | ons** | ons** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | \     | in    | Y     | Y     | Y     | \     | \     | \     |
|       |       | teger |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| H     | H     | de    | Y     | \     | \     | \     | \     | \     |
| EIGHT | eight | cimal |       |       |       |       |       |       |
|       | of    |       |       |       |       |       |       |       |
|       | t     |       |       |       |       |       |       |       |
|       | ower( |       |       |       |       |       |       |       |
|       | meter |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| TE    | Te    | v     | \     | \     | \     | \     | \     | \     |
| XTURE | xture | archa |       |       |       |       |       |       |
|       | of    | r(50) |       |       |       |       |       |       |
|       | tower |       |       |       |       |       |       |       |
|       | in    |       |       |       |       |       |       |       |
|       | clude |       |       |       |       |       |       |       |
|       | Q235  |       |       |       |       |       |       |       |
|       | Q345  |       |       |       |       |       |       |       |
|       | Q460  |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| CORR  | loss  | de    | \     | \     | \     | \     | \     | \     |
| OSION | ratio | cimal |       |       |       |       |       |       |
|       | of    |       |       |       |       |       |       |       |
|       | sect  |       |       |       |       |       |       |       |
|       | ional |       |       |       |       |       |       |       |
|       | area  |       |       |       |       |       |       |       |
|       | in    |       |       |       |       |       |       |       |
|       | ten   |       |       |       |       |       |       |       |
|       | yea   |       |       |       |       |       |       |       |
|       | rs.[  |       |       |       |       |       |       |       |
|       | ]{    |       |       |       |       |       |       |       |
|       | .Appl |       |       |       |       |       |       |       |
|       | e-con |       |       |       |       |       |       |       |
|       | verte |       |       |       |       |       |       |       |
|       | d-spa |       |       |       |       |       |       |       |
|       | ce}in |       |       |       |       |       |       |       |
|       | clude |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | [     |       |       |       |       |       |       |       |
|       |  ]{.A |       |       |       |       |       |       |       |
|       | pple- |       |       |       |       |       |       |       |
|       | conve |       |       |       |       |       |       |       |
|       | rted- |       |       |       |       |       |       |       |
|       | space |       |       |       |       |       |       |       |
|       | }in\[ |       |       |       |       |       |       |       |
|       | 0,1\] |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | \     |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| geom  | Geo   | \     | \     | \     | \     | \     | \     | \     |
|       | metry |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| WIR   | \     | \     | \     | \     | \     | Y     | \     | \     |
| ES_ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

\

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Col | *     | **T   | **Not | **U   | **Pr  | **Fo  | **Ch  | **E   |
| umn** | *Deta | ype** | null  | nique | imary | reign | eck** | xclus |
|       | ils** |       | c     | c     | key** | key** |       | ion** |
|       |       |       | ons** | ons** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | \     | in    | Y     | Y     | Y     | \     | \     | \     |
|       |       | teger |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| TRE   | vari  | v     | \     | \     | \     | \     | \     | \     |
| ETYPE | eties | archa |       |       |       |       |       |       |
|       | of    | r(50) |       |       |       |       |       |       |
|       | trees |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "A"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "B"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "C"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "D"   |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | "E"   |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| AGE   | How   | in    | \     | \     | \     | \     | \     | \     |
|       | old   | teger |       |       |       |       |       |       |
|       | of    |       |       |       |       |       |       |       |
|       | the   |       |       |       |       |       |       |       |
|       | tree  |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       |       |       |
|       | 1-100 |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| geom  | Geo   | \     | \     | \     | \     | \     | \     | \     |
|       | metry |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| \     | \     | \     | \     | \     | \     | \     | \     | \     |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

\

**SQL**

\

这部分内容应参考[postgis]{.s2}官方文档。

\

创建表之前需要创建数据库，应用[postgis]{.s2}扩展。

\

[Create table]{.s5}

\

QGIS[创建的]{.s4}polygon[和]{.s4}linestring[类型的要素类默认是]{.s4}multi[型的，所以创建表时]{.s4}geom[字段也要对应带]{.s4}multi[的类型。]{.s4}

\

(base) [jade_mayer]{.s6} in [\~/projects/lhx/asset/work/sql]{.s7}[
λ]{.s8} psql -d electric -f createtable_ucfsxxx.sql

\

[Create constraints]{.s5}

\

(base) [jade_mayer]{.s6} in [\~/projects/lhx/asset/work/sql]{.s7}[
λ]{.s8} psql -d electric -f createconstraints_ucfsxxx.sql

\

[Insert data]{.s5}

\

1\)

\

(base) [jade_mayer]{.s6} in [\~/projects/lhx/asset/work/sql]{.s7}[
λ]{.s8} shp2pgsql -a -s 32649 -I ../../data/electric/landusegrid.shp
ucfsxxx.landuse \> insertdata_ucfsxxx_landuse.sql

\

(base) [jade_mayer]{.s6} in [\~/projects/lhx/asset/work/sql]{.s7}[
λ]{.s8} psql -d electric -f insertdata_ucfsxxx_landuse.sql

\

2\)

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}shp2pgsql -a -s 32649 -I
../../data/electric/corridor.shp ucfsxxx.corridors \>
insertdata_ucfsxxx_corridors.sql

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}psql -d electric -f
insertdata_ucfsxxx_corridors.sql[ ]{.Apple-converted-space}

3\)

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}shp2pgsql -a -s 32649 -I
../../data/electric/lines.shp ucfsxxx.wires \>
insertdata_ucfsxxx_wires.sql [   ]{.Apple-converted-space}

Shapefile type: Arc

Postgis type: MULTILINESTRING\[2\]

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}psql -d electric -f
insertdata_ucfsxxx_wires.sql [   ]{.Apple-converted-space}

SET

SET

BEGIN

INSERT 0 1

INSERT 0 1

INSERT 0 1

CREATE INDEX

COMMIT

ANALYZE

\

4\)

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}shp2pgsql -a -s 32649 -I
../../data/electric/tower.shp ucfsxxx.towers \>
insertdata_ucfsxxx_towers.sql

[]{.s12}\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}psql -d electric -f
insertdata_ucfsxxx_towers.sql[   ]{.Apple-converted-space}

\

5\)

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}shp2pgsql -a -s 32649 -I
../../data/electric/trees.shp ucfsxxx.trees \>
insertdata_ucfsxxx_trees.sql[ ]{.Apple-converted-space}

\

(base) [╭]{.s4}─[jade_mayer]{.s9}[@]{.s10}[jadedeMacBook-Pro.local]{.s9}
**\~/projects/lhx/asset/work/sql** [ ]{.Apple-converted-space}

[╰]{.s4}─[➤]{.s11}[  ]{.Apple-converted-space}psql -d electric -f
insertdata_ucfsxxx_trees.sql [ ]{.Apple-converted-space}

\

[Query data]{.s5}

到此为止，数据库已经建好。接下来就是细化每个[decision]{.s13}，给出在数据库中的查询语句。

描述：新建三条输电线路，一条是东北[-]{.s13}西南走向，另外两条是西北[-]{.s13}东南走向。每条线路都要占用一定范围的土地，称为输电走廊。

**Decision 1**

在输电廊道和道路交叉口的两端要分别设置两个警示牌（每个交叉口共需要设置[4]{.s13}个警示牌），提醒过往行人车辆注意安全。请问修建这三条输电线路后总共需要设置多少个道路警示牌？

所属层：输电廊道层

**Decision 2**

\

假设只有居民区会统计人口数据，来评估三条输电廊道内会影响多少人的生活（某个居民区受影响人数按照通电廊道侵占居民区的面积占居民区的总面积比例换算）。输电廊道会经过的居民区的编号和人口数分别是？每个居民区受输电廊道影响面积占居民区总面积比例是多少？估算每个居民区受影响的人口分别是多少？

\

所属层：用地类型层

\

**Decision 3**

\

三条输电线路的材料费造价是多少？输电线路包括输电线缆和铁塔，一条线路可能有多条并行线缆。输电线缆材质类型[A]{.s2}，[B]{.s2}，[C]{.s2}的每公里价格分别是[3000]{.s2}，[
5000]{.s2}，[
7000]{.s2}；铁塔材质类型[Q235]{.s2}，[Q345]{.s2}，[Q460]{.s2}每个的价格分别为[6000]{.s2}，[
8000]{.s2}，[ 10000]{.s2}。我们可以提供的证据包括

每条线路的长度（公里）、材质、并行线路数、包含铁塔数、铁塔材质，这些证据对于该决策非常重要。

\

所属层：输电线路层

\

**Decision 4**

\

三条输电廊道的总占地面积是多少？由于三条输电廊道的规划，需要在现有用地规划的基础上新增多少面积的设施用地[(facilities)]{.s2}？这里认为输电廊道所在地需要规划为设施用地。

\

所属层：输电廊道层

\

\

**Decision 5**

\

输电廊道内都有哪些树种？分别有多少颗树？平均年龄各是多少？

\

所属层：输电廊道层

\

**Decision 6**

\

有多少颗树会因为修建输电线路而被砍掉？这些树的平均年龄是多少？假定离输电线缆直线距离[50m]{.s2}内的树要被砍掉。

\

所属层：输电线路层

\

**Decision 7**

\

每个铁塔在出厂时候厂家给出了该铁塔在[10]{.s2}年内的截面锈蚀率数据（[loss
ratio of sectional area in ten
years]{.s2}），请问在[10]{.s2}年后有多少个铁塔需要更换？假定锈蚀率大于[0.9]{.s2}的铁塔需要被更换？

\

所属层：输电线路层
