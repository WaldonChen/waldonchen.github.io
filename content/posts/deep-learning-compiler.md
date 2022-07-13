+++
title = "深度学习编译器"
author = ["Jun-Shi Chen"]
date = 2022-07-07T11:03:00+08:00
tags = ["tvm"]
categories = ["深度学习编译器"]
draft = false
tocNum = false
+++

本文整理深度学习编译器相关的论文和来自知乎等网站的相关材料<a href="#citeproc_bib_item_1">[1]</a>。


## <span class="section-num">1</span> 深度学习编译器相关论文 {#深度学习编译器相关论文}


### <span class="section-num">1.1</span> Survey {#survey}

-   The Deep Learning Compiler: A Comprehensive Survey

    > DL编译器的survey，总结了DL编译器的设计框架

-   An In-depth Comparison of Compilers for Deep Neural Networks on Hardware

    > 比较了Halide, XLA, TVM, TC等几种编译器的性能


### <span class="section-num">1.2</span> TVM系列 {#tvm系列}

<!--list-separator-->

1.  OSDI'18 - TVM: An Automated End-to-End Optimizing Compiler for Deep Learning

    文章<a href="#citeproc_bib_item_2">[2]</a>完整介绍了 TVM 的设计的背景，目标，技术难点和解决方案。该文章确定了整个 TVM 的技术架构，包括硬件无关的图级别的优化，硬件相关的算子优化，基于代价模型的搜索寻优等等。快速了解此文可以阅读已有的一些[论文阅读笔记](https://zhuanlan.zhihu.com/p/498115380)。

<!--list-separator-->

2.  IWMLPL'18 - Relay - A New IR for Machine Learning Frameworks

    Relay<a href="#citeproc_bib_item_3">[3]</a>是TVM 新的中间表示形式，不同框架的模型先转化成
    Relay，然后在Relay 上来做图优化。[如何评价TVM的新IR（Relay）？](https://www.zhihu.com/question/331611341/answer/875630325)

<!--list-separator-->

3.  Relay: A High-Level Compiler for Deep Learning<a href="#citeproc_bib_item_4">[4]</a>

    > TVM的第二代high-level IR，类似于编程语言，设计了语法规则，引入了let-binding机制。DL背景的开发者可以使用data flow graph来定义计算图，
    > PL(Program Language)背景的研究人员可以使用let binding来定义计算图。Let binding机制通过compute scope解决了AST的二义性问题。

    [Relay: A High-Level Compiler for Deep Learning 论文翻译](https://zhuanlan.zhihu.com/p/462831936)


### <span class="section-num">1.3</span> Auto-tuning相关工作 {#auto-tuning相关工作}

<!--list-separator-->

1.  NIPS'18 - Learning to Optimize Tensor Programs

    文章<a href="#citeproc_bib_item_5">[5]</a>发表于 2018 年的NIPS，详细介绍了autotvm 自动寻优方案。文章是对论文<a href="#citeproc_bib_item_2">[2]</a>的第5节的一个更加详细的扩充。主要观点在
    OSDI2018 的论文里都有描述，论文 1 没有涉及的的内容是引入了 transfer learning 的应用。

    [Learning to Optimize Tensor Programs解读](https://zhuanlan.zhihu.com/p/457573510)

<!--list-separator-->

2.  OSDI'20 - Ansor: Generating High-Performance Tensor Programs for Deep Learning

    Ansor 论文<a href="#citeproc_bib_item_6">[6]</a>发表于2020 年 OSDI ， 其核心目标是生成高效的程序，具体包括两个部分(1)如何扩大搜索空间(2)如何提高搜索的性能和效率。

    为了扩大搜索空间，改进了TVM 基于模板的搜索空间定义，通过层次化搜索的方案，解耦
    high-level 结构和low-level 细节。

    为了提升搜索的性能和效率，ansor 改进了TVM 的搜索策略，将搜索算法从模拟退火算法修改成了遗传算法(原文是进化搜索 evolutionary search，国内多翻译为遗传算法)，从而能够有效的跳出局部最优。

    > 把schedule分成sketch和annotation两层，sketch相当于TVM的schedule template，Ansor
    > 可以先搜索出sketch，再搜索annotation。

<!--list-separator-->

3.  FlexTensor: An Automatic Schedule Exploration and Optimization Framework for Tensor Computation on Heterogeneous System

    FlexTensor <a href="#citeproc_bib_item_7">[7]</a>

<!--list-separator-->

4.  CHAMELEON: ADAPTIVE CODE OPTIMIZATION FOR EXPEDITED DEEP NEURAL NETWORK COMPILATION


### <span class="section-num">1.4</span> Polyhedral {#polyhedral}

-   PLDI'21 - AKG: Automatic Kernel Generation for Neural Processing Units using Polyhedral Transformations <a href="#citeproc_bib_item_8">[8]</a>

    [PLDI 2021论文分析(一)：AKG-NPU上算子自动生成技术探索](https://zhuanlan.zhihu.com/p/384191216)

-   MICRO'20 - Optimizing the Memory Hierarchy by Compositing Automatic Transformations on Computations and Data <a href="#citeproc_bib_item_9">[9]</a>

    [53年来国内唯三，MindSpore加速昇腾芯片论文获国际顶会MICRO最佳论文提名](https://zhuanlan.zhihu.com/p/333394142)

<!--listend-->

-   [一.Poly基本原理及卷积分析示例](https://mp.weixin.qq.com/s/QEooKxP1sm5O90AUiqKQEQ)
-   [二. Poly在深度学习领域中发挥的作用](https://mp.weixin.qq.com/s/NRtud1UImE5ArZ2zQWFRyg)
-   [三. AI芯片上利用Poly进行软硬件优化的一些问题](https://mp.weixin.qq.com/s/bLBIrJb82IsnyoXSEr2xtw)

> 上面面三篇公众号文章介绍Poly的一些基本原理和在DL领域中的应用，作者是要术甲杰，是
> Poly研究领域的博士

-   [Polyhedral编译调度算法(1)------Pluto算法](https://zhuanlan.zhihu.com/p/199683290?utm_source=wechat_session&utm_medium=social&utm_oi=848584440992141312)

> 同样是要术甲杰写的介绍Pluto算法的文章


### <span class="section-num">1.5</span> Others {#others}

-   Tensorflow XLA/JAX
-   MLIR
-   GLOW @facebook
-   Halide
-   Tensor comprehension

-   [MLIR文章视频汇总](https://zhuanlan.zhihu.com/p/141256429?utm_source=wechat_session&utm_medium=social&utm_oi=837261071604645888&wechatShare=1&s_r=0)

-   [Multi-Level Tactics: Abstraction Raising in Multi-Level IR](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf)

-   [FUSIONSTITCHING: DEEP FUSION AND CODE GENERATION FOR TENSORFLOW COMPUTATIONS ON GPUS](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/FusionStitching.pdf)

> 用shared memory来实现更激进的operator fusion策略

-   [Automatic differentiation in ML: Where we are and where we should be going](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/AutoDiffinML.pdf)
-   [Automatic Differentiation in Machine Learning: a Survey](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/AutoDiffSurvey.pdf)

> 两篇关于自动微分的survey

-   [IREE: MLIR-based End-to-End ML Tooling](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/IREE.pdf)

> schedule和execution阶段进行联合优化

-   [AI编译优化--总纲](https://zhuanlan.zhihu.com/p/163717035)
-   [访存密集算子优化](https://zhuanlan.zhihu.com/p/163857096)
-   [计算密集算子优化](https://zhuanlan.zhihu.com/p/174817186)
-   [AI编译优化--业务实践](https://zhuanlan.zhihu.com/p/194353051)

> 阿里杨军的系列文章

-   [swTVM: Exploring the Automated Compilation for Deep Learning on Sunway Architecture](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/swTVM.pdf)

> 用TVM在神威超算上生成算子

-   [TensorFlow Graph Optimizations](https://github.com/MondayYuan/DLCompilerResource/blob/master/pdf/TFGraphOptimizationsStanford.pdf)

> TensorFow中的图优化


## <span class="section-num">2</span> 其它相关文档 {#其它相关文档}


### <span class="section-num">2.1</span> [AI编译器@金雪峰](https://www.zhihu.com/people/jin-xue-feng) {#ai编译器-金雪峰}

-   [AI编译器的概览、挑战和实践](https://zhuanlan.zhihu.com/p/508345356)
-   [针对神经网络的编译器和传统编译器的区别和联系是什么？](https://www.zhihu.com/question/396105855/answer/1868408680)

    [深度学习编译器系列之嵌入在 AI 框架中的深度学习编译器](https://zhuanlan.zhihu.com/p/342865488)


### <span class="section-num">2.2</span> [漫游深度学习编译器@知乎](https://www.zhihu.com/column/c_1388629436179378176) {#漫游深度学习编译器-知乎}

-   [TVM系列「一」TVM概览](https://zhuanlan.zhihu.com/p/381324332)
-   [TVM系列「二」TVM学习资源](https://zhuanlan.zhihu.com/p/381330616)
-   [TVM系列「三」TVM官方文档的结构](https://zhuanlan.zhihu.com/p/381331888)
-   [TVM系列「四」TVM的使用：compute+schedule双剑合璧](https://zhuanlan.zhihu.com/p/381333188)
-   [TVM系列「五」TVM整体架构及其代码生成](https://zhuanlan.zhihu.com/p/381691430)
-   [TVM系列「六」Relay IR与Relay Pass](https://zhuanlan.zhihu.com/p/390087648)
-   [TVM系列「七」AutoTVM（AutoTune）](https://zhuanlan.zhihu.com/p/392015642)
-   [TVM系列「八」AutoScheduler「Ansor」](https://zhuanlan.zhihu.com/p/394765523)


### <span class="section-num">2.3</span> [TVM代码走读【@知乎专栏】](https://www.zhihu.com/column/c_1254058636869603328) {#tvm代码走读-知乎专栏}

-   [TVM代码走读（一） ONNX前端](https://zhuanlan.zhihu.com/p/145676823)
-   [TVM代码走读（二） 算子实现](https://zhuanlan.zhihu.com/p/149386093)
-   [TVM代码走读（三） 图优化1--初识PASS](https://zhuanlan.zhihu.com/p/149988448)
-   [TVM代码走读（四） 图优化2--TVM RELAY树结构](https://zhuanlan.zhihu.com/p/151351056)
-   [TVM代码走读（五） 图优化3-- Constant Folding](https://zhuanlan.zhihu.com/p/151815380)
-   [TVM代码走读（六） 图优化4-- Fuse ops](https://zhuanlan.zhihu.com/p/153098112)
-   [TVM代码走读（七） 模型编译1--调用链](https://zhuanlan.zhihu.com/p/161195053)
-   [TVM代码走读（八） 模型编译2--编译优化](https://zhuanlan.zhihu.com/p/165236267)
-   [TVM代码走读（九） 计算和调度](https://zhuanlan.zhihu.com/p/166551011)
-   [TVM代码走读（十） AutoTvm](https://zhuanlan.zhihu.com/p/181399538)
-   [TVM代码走读（十一） te::Stage](https://zhuanlan.zhihu.com/p/208594323)
-   [TVM代码走读（十二） lower--phase 0](https://zhuanlan.zhihu.com/p/202938038)
-   [TVM代码走读（十三） arith::analyzer](https://zhuanlan.zhihu.com/p/245453441)
-   [TVM代码走读（十四） lower--ScheduleOps](https://zhuanlan.zhihu.com/p/257128533)
-   [TVM代码走读（十五） lower--relay func到lower的流程梳理](https://zhuanlan.zhihu.com/p/263581574)
-   [TVM代码走读（十六） lower--phase0后续流程](https://zhuanlan.zhihu.com/p/267986568)
-   [TVM代码走读（十七） lower--phase 1](https://zhuanlan.zhihu.com/p/275708458)
-   [TVM代码走读（十八） lower--LoopPartition(phase 2)](https://zhuanlan.zhihu.com/p/307689224)


### <span class="section-num">2.4</span> [深度学习编译器@柳嘉强](https://www.zhihu.com/people/liu-jia-qiang-18-27) {#深度学习编译器-柳嘉强}

-   [7. 深度学习编译器 - 算子的高效实现](https://zhuanlan.zhihu.com/p/511043383)
-   [6. 深度学习编译器 - 低精度计算之量化](https://zhuanlan.zhihu.com/p/469972467)
-   [5. 深度学习编译器 - 图优化（续)](https://zhuanlan.zhihu.com/p/436025551)
-   [5. 深度学习编译器-图优化](https://zhuanlan.zhihu.com/p/412217136)
-   [4. 深度学习编译器-自动微分](https://zhuanlan.zhihu.com/p/344752857)
-   [3. 深度学习编译器 - 图表示](https://zhuanlan.zhihu.com/p/338299844)
-   [2. 深度学习编译器 - 前端](https://zhuanlan.zhihu.com/p/309793908)
-   [1. 深度学习编译器-引言](https://zhuanlan.zhihu.com/p/307750772)

## &#21442;&#32771;&#25991;&#29486;

<style>.csl-left-margin{float: left; padding-right: 0em;}
 .csl-right-inline{margin: 0 0 0 1em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>
    <div class="csl-left-margin">[1]</div><div class="csl-right-inline">陈逢锦, “Tvm及深度学习编译器相关论文,” 2022. <a href="https://zhuanlan.zhihu.com/p/500041871">https://zhuanlan.zhihu.com/p/500041871</a> (accessed May 03, 2022).</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>
    <div class="csl-left-margin">[2]</div><div class="csl-right-inline">T. Chen <i>et al.</i>, “TVM: an automated end-to-end optimizing compiler for deep learning,” in <i>13th USENIX symposium on operating systems design and implementation, OSDI 2018, carlsbad, ca, usa, october 8-10, 2018</i>, 2018, pp. 578–594. Available: <a href="https://www.usenix.org/conference/osdi18/presentation/chen">https://www.usenix.org/conference/osdi18/presentation/chen</a></div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>
    <div class="csl-left-margin">[3]</div><div class="csl-right-inline">J. Roesch <i>et al.</i>, “Relay: a new ir for machine learning frameworks,” in <i>Proceedings of the 2nd acm sigplan international workshop on machine learning and programming languages</i>, 2018, p. nil. doi: <a href="https://doi.org/10.1145/3211346.3211348">10.1145/3211346.3211348</a>.</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>
    <div class="csl-left-margin">[4]</div><div class="csl-right-inline">J. Roesch <i>et al.</i>, “Relay: A High-Level Compiler for Deep Learning,” 2019.</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_5"></a>
    <div class="csl-left-margin">[5]</div><div class="csl-right-inline">T. Chen <i>et al.</i>, “Learning to optimize tensor programs,” in <i>Proceedings of the 32nd international conference on neural information processing systems</i>, 2018, pp. 3393–3404.</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_6"></a>
    <div class="csl-left-margin">[6]</div><div class="csl-right-inline">L. Zheng <i>et al.</i>, “Ansor: Generating high-performance tensor programs for deep learning,” in <i>14th USENIX symposium on operating systems design and implementation, OSDI 2020, virtual event, november 4-6, 2020</i>, 2020, pp. 863–879. Available: <a href="https://www.usenix.org/conference/osdi20/presentation/zheng">https://www.usenix.org/conference/osdi20/presentation/zheng</a></div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_7"></a>
    <div class="csl-left-margin">[7]</div><div class="csl-right-inline">S. Zheng, Y. Liang, S. Wang, R. Chen, and K. Sheng, “Flextensor,” in <i>Proceedings of the twenty-fifth international conference on architectural support for programming languages and operating systems</i>, 2020, p. nil. doi: <a href="https://doi.org/10.1145/3373376.3378508">10.1145/3373376.3378508</a>.</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_8"></a>
    <div class="csl-left-margin">[8]</div><div class="csl-right-inline">J. Zhao <i>et al.</i>, “Akg: automatic kernel generation for neural processing units using polyhedral transformations,” in <i>Proceedings of the 42nd acm sigplan international conference on programming language design and implementation</i>, 2021, p. nil. doi: <a href="https://doi.org/10.1145/3453483.3454106">10.1145/3453483.3454106</a>.</div>
  </div>
  <div class="csl-entry"><a id="citeproc_bib_item_9"></a>
    <div class="csl-left-margin">[9]</div><div class="csl-right-inline">J. Zhao and P. Di, “Optimizing the memory hierarchy by compositing automatic transformations on computations and data,” in <i>2020 53rd annual ieee/acm international symposium on microarchitecture (micro)</i>, 2020, p. nil. doi: <a href="https://doi.org/10.1109/micro50266.2020.00044">10.1109/micro50266.2020.00044</a>.</div>
  </div>
</div>
