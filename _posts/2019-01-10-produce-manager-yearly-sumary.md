---
layout: post
title: 工作总结复盘 - 产品
category: product
tags: 
---
![](https://cdn.kelu.org/blog/tags/interview.jpg)

> 偶然翻到这篇文章，讲的蛮好，转载做个记录。原文：<https://mp.weixin.qq.com/s/ydbYFdmcLryAwbu9TwsxoQ>

18年10月换了新工作，对比美团和同程的工作经历，觉得之前却是温室里的花朵，一切都在有条不紊的环境下进行。而现在快速增长的业务，公司以每周新进7-10人的速度快速扩张，经验、认知和能力一次次受到挑战，压力还是蛮大的。逻辑不严谨致产品设计质量不高而心情低落时长有，但也需要不断构筑自信心，安慰自己接下来提高。这个过程中需要不断地学习、总结与反思，也体现了环境对于产品经理的影响，不同环境下，产品经理的价值和成长速度迥然不同。

一直看好互联网行业是块香饽饽，工作不愁，却没想2018年互联网进入了寒冬时代。年中开始，小米、美团、拼多多、同程相继上市；年底，很多公司面临裁员或组织架构调整，身边的朋友有受到波及的，才意识到这些都是真正发生在自己身边。我们公司还在不断拓展新业务并于年前拿到蚂蚁金服D轮融资，个人觉得还是蛮幸运的，也对面试时认可我的领导表示深深的感恩。

**产品流程滚瓜烂熟，产品理论一套一套，但在这两个多月的时间内，实际工作却不是那么回事儿，慢慢也暴露了越来越多的问题，自己对产品工作流程的各个节点有一些新的认识和感触，故作此总结。**

**一、需求分析之识别真需求**

产品是需求输出的源头，我们会接到来自各方的需求：运营或客服反馈、老板或leader的个人想法、业务发展或产品本身的迭代功能......之前项目，从需求收集到需求输出，做的最多的是评估需求价值，即这个需求到底有没有必要做，做了之后可以为我们带来什么？而现在需要考虑更多的是：需求真正是为了解决了什么问题？是否有可替代的更好的方案？而不是用户或客服反馈说，简单的添加一个什么样的功能？或把这个功能改成什么样式？**用户想要什么不等于真实需求；可以怎么做不等于应该怎么做。需求分析理论我们都知道，如何把理论在实际工作中真正应用起来，是这个阶段我感悟最深的一点。**

我在实际项目中，根据客服反馈，将余额提现失败的转人工做成了一个需求，开发到一半，才发现客服要求转人工的真正目的是用户风险验证FaceBook找不回的原因，应该要解决FaceBook账号找不回的问题，而不是客服反馈说把提现申请失败的转到人工审核中，让客服操作提现申请成功。

**二、产品设计之竞品分析**

面试的时候，我们会被问到一个问题：你有没有了解过你行业的其他竞品？如果你说没有，那面试分数将直接下降。包括面试的这家公司的行业竞品，比如，我当时去来电科技面试时，面试官问到我对来电和街电的看法。**我认为：做产品设计时竞品分析是必须要做的一件事儿。大到项目立项时的竞品行业分析、产品战略，小到产品设计时具体的某个功能，你都要去借鉴，去对比，去分析。**如果竞品没有直接显现的功能，需要触发某个条件才能发生，那么你就要把自己当作一个用户，去体验它的完整流程。

有这样的感悟，是因为自己近期做了一个“还款提醒”功能。作为用户，没有借款过、逾过期，所以第一版的推送频率和文案都是自己YY的，后面同事提到，你应该自己去体验一下这个流程，才知道有更好的优化方向，这才意识到竞品分析必须要放到产品的设计流程中来。

产品设计的过程中，也需要考虑：

- 是否需要UE、UI稿输出？

- 是否考虑了异常情况，边界情况？

- 流程是否形成了闭环？

  在新增一个功能时特别要注意对其他模块的影响，最好的做法就是把自己当作用户，反复体验整个流程，关注点不能只在新增的功能点上。

- 是否需要新旧版本兼容？

- 是否有利于功能延展，版本迭代？

- 上线后若出现BUG、异常、效果不明显、影响流程、影响体验，是否可及时根据已有逻辑控制风险（如该功能有配置开关、可通过下线banner、关闭入口解决）

- 是否需要A/B test？

- 是否需要数据埋点？

上述提到的每一点在产品设计过程中都是应该考虑的（如果有需要补充的，欢迎后面留言讨论）。

**三、文档撰写之条理清晰**

因目前负责模块较之前更复杂一些，且大多数都是在已有的功能上做重构或优化，PRD文档在开发的过程中一次又一次被挑出描述不清楚，尤其是写类似“和XXX功能保持一致”这样的话。事实上，之前做XXX功能的开发同事和目前做新需求的往往不是一个人，他们不能确定"XXX功能"到底是怎么样的？

**在已有的功能上做重构或优化，需要在文档中讲述新的需求是新增、删除还是更新之类的；同时文案也要易懂，不存在歧义。原型上，需要标明当前页是从哪个页面或哪个按钮跳转来的？当前页返回，又是回到了哪个页面？同样得，弹窗上的按钮，“取消”也好，“确认”也罢，必须要写清楚点击后的效果。是又发生了页面跳转还是停留当前页？**

我们目前的App，因之前原型设计时，对页面或按钮跳转没有说明，导致同样的功能，安卓和IOS跳转到不同的页面，两边的开发在实际开发过程中根据自己的理解“自定义”跳转。

**四、需求评审之背景讲解**

之前需求评审时一上来就跟开发讲功能点：我需要一个什么功能，这个功能应该做成什么样子。如果开发不了解需求背景或需求目的，他们就真的只会按照原型原封不动的去“实现”出来，**但如果他们了解需求背景，也会有自己的思考，去看这个功能合不合理，或以一种可拓展性更强的方式来实现。**

**五、项目跟进之快速解决问题**

需求评审完以后，进到开发环节。在实际开发过程中，具体的细节问题往往比自己想像的多很多。也经常发生：用A方案好还是B方案好？**这个时候需要产品的判断力和决策力，你必须自己能做主，在最快的时间内拍板，到底采用哪种方案，这是快速解决问题的能力。**项目上线后，线上产品出现异常，你能最快找到问题并协调开发将问题解决。这些在目前项目中时长发生，也是在这个过程中，慢慢学会分析问题原因的能力。

童年时，我会为了一颗糖果，能和妈妈赌气一天；

中学时，我会为了一份成绩，能奋笔疾书一整年；

高中时，我会为了一道难题，能苦思冥想一星期；

大学时，我会为了一个笑容，能心里美美一辈子；

工作后，我会为了一个失误，而难过郁闷好一会。

换了新工作后，996是常事，周末外出几次最后又回到公司看数据解决问题。比如上周末从草莓园回来，因线上产品出了问题，下午四五点又回公司解决问到到晚上十点多，朋友调侃我拿一天当两天用，才意识到，咦？这一天真是又玩了又工作了。

但是从没后悔过，也不羡慕看剧吃饭逛街的清闲生活，反而很兴庆，工作的满足感远远超过了辛苦和疲倦，甚至超过了当初爱情带来的短暂的幸福感。人在年轻的时候就应该竭尽全力去做自己想做的事儿，包括工作。**我愿意用现在这般辛苦，换取一个无怨无悔的人生。**

------

 / END.