---
title: R语言学习 - 非参数法生存分析
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - R
  - Bioinfo
---

生存分析指根据试验或调查得到的数据对生物或人的生存时间进行分析和推断，研究生存时间和结局与众多影响因素间关系及其程度大小的方法，也称生存率分析或存活率分析。常用于肿瘤等疾病的标志物筛选、疗效及预后的考核。

<mark>简单地说，比较两组或多组人群随着时间的延续，存活个体的比例变化趋势。活着的个体越少的组危险性越大，对应的基因对疾病影响越大，对应的药物治疗效果越差。</mark>

生存分析适合于处理时间-事件数据，如下

![](http://blog.genesino.com/images/surv_input_data.png)


生存时间数据有两种类型：

* 完全数据 (complete data)指被观测对象从观察起点到出现终点事件所经历的时间; 一般用状态值1或TRUE表示。
* 截尾数据 (consored data)或删失数据，指在出现终点事件前，被观测对象的观测过程终止了。由于被观测对象所提供的信息是不完全的，只知道他们的生存事件超过了截尾时间。截尾主要由于失访、退出和终止产生。一般用状态值0或FALSE表示。
* TCGA中的临床数据标记也符合这个规律，在下面软件运行时也可修改状态值的含义。

生存概率 (survival probability)指某段时间开始时存活的个体至该时间结束时仍然存活的可能性大小。

`生存概率=某人群活过某段时间例数/该人群同时间段期初观察例数。`

生存率 (Survival rate)，用`S(t)`表示，指经历`t`个单位时间后仍存活的概率，若无删失数据，则为活过了`t`时刻仍然存活的例数/观察开始的总例数。如果有删失数据，分母则需要按时段进行校正。

生存分析一个常用的方法是寿命表法。

寿命表是描述一段时间内生存状况、终点事件和生存概率的表格，需计算累积生存概率即每一步生存概率的乘积 (也可能是原始生存概率)，可完成对病例随访资料在任意指定时点的生存状况评价。

![](http://blog.genesino.com/images/surv_life_table.png)

### R做生存分析

R中做生存分析需要用到包`survival`和`survminer`。输入数据至少两列，`存活时间`和`生存状态`，也就是测试数据中的`Days.survial`和`Status`列。如果需要比较不同组之间的差异，也需要提供个体的分组信息，如测试数据中的`Clinic`列。对应TCGA的数据，一般根据某个基因的表达量或突变有无对个体进行分组。

读入数据

```
library(survival)
addicts <- read.table('ADDICTS.txt', sep="\t", header-T)
Error in read.table("ADDICTS.txt", sep = "\t", header - T) : 
  object 'header' not found
addicts <- read.table('ADDICTS.txt', sep="\t", header=T)
head(addicts)
  ID Clinic Status Days.survival Prison Dose
1  1      1      1           428      0   50
2  2      1      1           275      1   55
3  3      1      1           262      0   55
4  4      1      1           183      0   30
5  5      1      1           259      1   65
6  6      1      1           714      0   55
summary(addicts)
       ID             Clinic          Status       Days.survival   
 Min.   :  1.00   Min.   :1.000   Min.   :0.0000   Min.   :   2.0  
 1st Qu.: 65.25   1st Qu.:1.000   1st Qu.:0.0000   1st Qu.: 171.2  
 Median :131.50   Median :1.000   Median :1.0000   Median : 367.5  
 Mean   :134.13   Mean   :1.315   Mean   :0.6303   Mean   : 402.6  
 3rd Qu.:205.75   3rd Qu.:2.000   3rd Qu.:1.0000   3rd Qu.: 585.5  
 Max.   :266.00   Max.   :2.000   Max.   :1.0000   Max.   :1076.0  
     Prison            Dose      
 Min.   :0.0000   Min.   : 20.0  
 1st Qu.:0.0000   1st Qu.: 50.0  
 Median :0.0000   Median : 60.0  
 Mean   :0.4664   Mean   : 60.4  
 3rd Qu.:1.0000   3rd Qu.: 70.0  
 Max.   :1.0000   Max.   :110.0
```

计算寿命表

```
# Days.survival：跟踪到的存活时间
# Status: 跟踪到的存活状态
# ~1表示不进行分组
fit <- survfit(Surv(Days.survival, Status)~1, data=addicts)

# 获得的survial列就是生存率 
summary(fit)
Call: survfit(formula = Surv(Days.survival, Status) ~ 1, data = addicts)

 time n.risk n.event survival std.err lower 95% CI upper 95% CI
    7    236       1    0.996 0.00423       0.9875        1.000
   13    235       1    0.992 0.00597       0.9799        1.000
   17    234       1    0.987 0.00729       0.9731        1.000
   19    233       1    0.983 0.00840       0.9667        1.000
   26    232       1    0.979 0.00937       0.9606        0.997
   29    229       1    0.975 0.01026       0.9546        0.995
   30    228       1    0.970 0.01107       0.9488        0.992
   33    227       1    0.966 0.01182       0.9431        0.989
   35    226       2    0.957 0.01317       0.9320        0.984
   37    224       1    0.953 0.01379       0.9265        0.981
   41    223       2    0.945 0.01493       0.9158        0.974
   47    221       1    0.940 0.01546       0.9105        0.971
   49    220       1    0.936 0.01597       0.9053        0.968
   50    219       1    0.932 0.01646       0.9001        0.965
   59    216       1    0.927 0.01694       0.8949        0.961
   62    215       1    0.923 0.01740       0.8897        0.958
   67    213       1    0.919 0.01785       0.8845        0.954
```

绘制生存曲线，横轴表示生存时间，纵轴表示生存概率，为一条梯形下降的曲线。下降幅度越大，表示生存率越低或生存时间越短。

```
library(survminer)
# conf.int：是否显示置信区间
# risk.table: 对应时间存活个体总结表格
ggsurvplot(fit, conf.int=T,risk.table=T)
```

![](http://blog.genesino.com/images/surv_km_all.png)


根据`Clinic`属性对病人进行分组，评估比较两组之间生存率的差别。

```
# 首先把数字形式转成因此形式
addicts$Clinic <- factor(addicts$Clinic)
# 按Clinic分组
fit <- survfit(Surv(Days.survival, Status)~Clinic, data=addicts)
# 绘制曲线
ggsurvplot(fit, conf.int=T,risk.table=T, risk.table.col="strata", pval=T)
```

![](http://blog.genesino.com/images/surv_km_all_clinic.png)

测试数据下载; [ADDICTS.txt](http://blog.genesino.com/images/ADDICTS.txt.zip)

