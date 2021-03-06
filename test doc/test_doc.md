# 测试计划

## 编写目的
在开发大型软件的漫长过程中，面对及其错综复杂的问题，人的主观认识不可能完全符合客观现实，与工程密切相关的各类人员之间的通信和配合也不可能完美无缺。因此，在软件生命周期的每个阶段都不可避免地会产生差错。尤其对于计算器计算这样基础又重要的软件，必须保证计算的结果在给定的范围和精度内毫无差错，保证人的计划和生命财产安全不受损失。测试是“为了发现程序中的错误而执行程序的过程”。测试的目的在于在软件投入生产性运行之前，尽可能多的发现软件中的错误。目前软件测试仍然是保证软件质量的关键步骤，它是对软件规格说明、设计和编码的最后复审，也是必不可少的关键步骤。
##项目背景
本项目由小组成员 郑非，邢宇，钱劲翔 负责开发
需求文档负责人：钱劲翔
编码负责人：郑非
测试负责人：邢宇
## 参考资料
- WPF教程与资料
- C#教程与资料
- 数值计算教程与资料

## 任务概述
### 目标
测试是“为了发现程序中的错误而执行程序的过程”，测试的目的就是在软件投入生产性运行之前，尽可能多地发现软件中的错误。
#### 运行环境
本程序由VS2015编辑、调试运行与windows平台下
### 需求概述
实现科学计算器的基础和高级功能。类似于简单算术运算和函数求值，微积分等。

## 计划
### 测试方案
测试方案是测试阶段的关键技术问题。为了提高测试效率降低测试成本，本测试方案采用黑盒法设计的基本测试方案。在用黑盒法测试的过程中，将数据的输入和输出与mathematica的部分输出作对比，重点进行边界和精度测试方面的考量。

## 测试项目说明
### 测试项目名称及测试内容
在测试过程中，需要对各计算函数进行测试。对计算函数的精度及边界情况进行测试，并最后进行性能上的考量，以及报错信息提示。
各模块测试名称如下：
* 基本加减乘除乘方开根运算
* 初等函数运算
* 微积分运算		

## 测试输入		
* 基本运算功能 

	输入：1/7
	输出：0.1428571429
	精度：10^-10
	性能：< 1s
**************
	输入：10^20\*10^20
	输出：10000000000000000000000000000000000000000.0000000000
**************
	输入：10^1000\*10^1000
	输出：∞
	精度：能接受的大数上限大概在10^300
	分析：缺乏必要的位分割和科学计数法表示支持
**************
* 微积分功能

微分功能
	
	输入：diff( sin( cos( sin(x) ) ), 2)
	输出：0.2683363637
	对比输出：0.2683
	精度：.< 10^-4
	性能：<1s
	分析：只能在给定点出求一阶微分值，并且对输入没有输入格式提示 
**************
	输入：diff(diff(x^2,1),2)
	输出：0.000000000
	分析:嵌套求导没有问题
***************
积分功能

	输入：int(2,3,x)	
	积分分割次数：100000
	输出：2.499995000
	对比输出：2.5
	精度：> 10^-6
	性能：<1s
**************
	积分分割次数：1260460
	输出：2.5000017596
	对比输出：2.5
	精度：~ 10^-6
	性能：<1s
	分析：没有在合理的精度内舍入,缺乏输入格式提示；
		 正常符号计算软件输入格式为（以mma为例）Integrate[f,{x,xmin,xmax}], 但是本软件输入方式为int(xmin,xmax,f)
**************
	输入：int(1,2,int(2,3,x))
	积分分割次数：100000
	输出：0.0000250000
	对比输出：2.5
	分析：无法嵌套积分
***************
求和函数

	输入：sum(1,3,x)
	输出：6.0000000000
**************
	输入：sum(4,4,x)
	输出：4.0000000000
	输入：sum(5,4,x)	
	输出：0.0000000000
	精度：在整数的范围内精度内求和无误差
	结论：求和功能完善
**************
* 初等函数功能
	
	输入：-1/0
	输出：-∞
**************
	输入：0/0
	输出：NaN
**************
	输入：Ln（0）
	输出：-∞
**************
	输入：tan(pi/2)
	输出：16331778728383800.0000000000
**************
	输入：sqrt(-1)
	输出：NaN
**************
	输入：arcisn(1)*2	
	输出：3.1415926536
**************
	输入：log(100)
	输出：2	（只支持10为底的对数）
**************
	输入：int(-10000000,10000000,e^(-x^2))		
	精度：积分分割次数100000
	输出：200
	运行时间：<1s

	精度：积分分割次数为181659979
	输出：1.7724538509
	运行时间： 38s
**************
* 报错提示
- 对未定义字符和运算报错
- 对输入格式不符合要求的有”在..内缺少缺少一个逗号“的报错

## 测试结果及分析报告
### 软件能力
经测试，该软件实现了绝大多数计算器所具有的基本功能，具有一定的科学计算能力，也可以达到必要的精度
### 缺陷和限制
- 可以达到比较高的精度，但是需要较长的程序运行时间。对于某些明显的整数解缺乏必要的舍入
- 程序的输入格式提示不太明朗，缺乏相应的输入格式提示或用户手册
- 对于一些函数可以做到对边界比如无穷情况的考虑，比如Ln(0),但是某些函数缺乏必要的无穷支持比如tan(pi/2)
### 建议
- 增加输入格式的提示框
- 完善报错机制
- 自动选取分割次数，改善精度
- 提高适当精度要求下的性能和运行时间
- 规范报错，为输入格式提供建议
### 测试结论
该软件在各方面的综合能力合格，通过！


