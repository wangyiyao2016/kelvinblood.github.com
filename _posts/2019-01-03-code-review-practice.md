---
layout: post
title: Code Review - Leancloud & coolshell
category: tech
tags: github
---

![](https://cdn.kelu.org/blog/tags/github.jpg)

> 最近在阅读 kubernetes 的代码，顺着看了部分 code review 的文章，蛮有意义的，转载过来留个记录。原文来自：[如何有效地做 Code Review - Leancloud](https://zhuanlan.zhihu.com/p/19967954)，[从CODE REVIEW 谈如何做技术 - coolshell](https://coolshell.cn/articles/11432.html)

# 意义

不少开发团队和创业公司都在纠结是否要执行 code review，既希望改进代码质量，又担心带来的负担会拖慢项目进度。实时上，在软件开发中质量和效率往往并不是二选其一的关系。能产出高质量代码的团队通常效率也非常高。

在我作为工程师的职业经历中，自动化测试和 code review 可说是能**同时**提高代码质量和开发效率的两个最有效的手段。所谓 code review，和学术界的 peer review 类似。Peer review 是由同事或同行对一位作者的作品进行查阅并提出建议和问题，只有当所有提出的问题都得到满意的答案后，作品才能发表。对于 code review 来说，作品就是代码，发表就是把代码 commit 到官方代码库。

在 Code Complete 这本书中讲述了两个很有说服力的案例。在一项对同一个团队开发的很多个程序进行对比的研究中，没有经过 review 的程序平均每 100 行有 4.5 个错误，而经过 review 的程序平均每 100 行只有 0.82 个错误，也就是说 80% 的错误在 review 中被修正了。AT & T 的一个 200 多人的部门在开始执行 code review 后，开发效率提高了 14%，而错误减少了 90% 左右。

除了减少缺陷，避免在诊断错误上浪费时间，review 的过程还可以通过相互的督促保证代码有好的可读性、文档、风格，并同时检查测试覆盖率等开发过程中的规范，从而提高团队的协作效率。对于所有复杂的事情来说，总是越早发现问题，解决问题的成本越低。

对于经验不足或者刚开始一份新工作的人来说，通过 code review 可以得到更资深的人帮助，更快熟悉现有的规范和架构，在新的环境和团队中快速提升。

对于资深的工程师来说，让其他同事 review 代码，有利于在团队中传播经验、知识和好的实践。身边的同事水平提高会让自己的工作也更高效。并且谁都有需要休假的时候，无论是公司还是个人都不希望有太多工作因此而停滞，如果有平时就熟悉自己工作的同事，这个问题就很好解决。

像很多其他事情一样，code review 最难的就是迈出第一步**。**一旦开始，花在 review 过程的每一分钟都会很快被成倍地赚回来。如果你不在一个可以一下改变团队流程的位置上，那么至少可以和认同这件事的少数同事先开始实践，当价值开始体现的时候，相信其他人会乐于效仿。

# 如何开始

**使用方便的工具**。要在团队中成功推行 code review，有好的工具是很重要的。谁都不愿意在工作中加入繁琐的过程，所以如果要让人接受一个新的步骤，最好让它有尽可能好的体验。在我用过的开源 code review 工具中，Phabricator 是最完善的。Review Board 应该也是不错的选择，只是我很久没实际用了，不知道最新状态。GitHub 在支持 side-by-side diff 后，它的 pull request 也提供了很好的 code review 体验，唯一不足的是无法从机制上强制所有 commit 都经过 pull request 的过程。

**把简单的检查自动化**。有很多检查是可以自动化的，比如一些风格规范（缩进、空行、行尾空格、命名等），这类问题应该尽可能写脚本检查。一方面可以让负责 review 的工程师把更多注意力放在更高层面的问题上；另一方面，从接受 review 的人心理上说，由程序提出这些细节问题比让另一个人来挑刺要更容易接受些。当然，这并不是说人工 review 的时候应该忽略细节问题。

**控制每次 review 的代码量**。每次 review 包含 200 行左右代码是比较理想的，最多不要超过 400 行。因为如果代码太多，review 的人容易因为注意力分散而忽略一些问题，另外也可能让时间拖得过长。因此，开发的时候需要把大的改动分解成多个小的步骤，每完成一个步骤就提交一次 review。

**使用异步的工作流**。这和上一点是相关的，当你需要把一个改动分为相互依赖的多步时，不应该因为等待 review 而 block 住自己的工作。在当前分支等待 review 时，可以从这个点开一个新的分支继续开发，之后再把 review 完的分支 merge 进来。

**作者应该提供清晰的 commit note**。Code review 的重要作用之一是同事间的交流，每个 commit 的 commit note 很重要也很影响 review 的效率，应该包含这个改动的目的，以及实现方式的概述。如果使用的 review 系统支持对 review 本身的描述（如 GitHub 的 pull request），那么应该写清楚作者希望 reviewer 重点关注的问题。

**在合并到主干之前进行 review**。有的人主张小团队应该做事后的 review，因为这样效率更高、更「轻量」。事实上，这样并不会减少工作量，并且如果工作流安排合理，事前 review 并不会导致效率降低。从心理上说，代码并合并到主干之后往往就意味着「完事了」，在时间比较紧张的时候很难坚持 review 所有代码。所以应该把 code review 作为代码合并到主干前必过的一道关口。

**所有人的代码都要经过 review**。Code review 并不是资深工程师对初级工程师做的事情，而应该全员平等参与，每个人都会有所收获。关于这方面在上一篇「[为什么每个团队都需要 Code Review](http://zhuanlan.zhihu.com/leancloud/19962430)」里也有提及。

**关注设计方面的问题和客观的规范，避免在主观意见上争执**。Code review 的讨论应该专注于设计层面的问题以及在团队中有明确共识的规范（代码风格，测试覆盖等），而要避免在一些主观意见的分歧上浪费时间。这也意味着应该在一些本身不重要，但很影响一致性的细节上尽早达成有共识的规范，如缩进方式，括号的位置等等，避免在 review 中去争论这些问题。

**从正面看待在 review 中发现的问题**。当发现一个错误时，并不应该看作是一个人犯了错被另一个人发现了，而是两个人配合改进了代码、避免了错误。

**Review 所有的代码，包括很简单的改动**。每一个 commit，无论多小都应该经过 review。一方面，很难界定什么算简单的改动，如果一行的 commit 不用 review，那两行是不是差不多同样简单，三行呢？另一方面，我已经不记得自己曾有多少次觉得「这个改动太简单，不用跑测试就可以提交了」，然后很快因为测试通不过而很尴尬地被别人 rollback。所以无论多小的改动都应该有测试、都应该通过 review。

**循序渐进**。如果现在完全没有做 code review，那么到整个团队都能严格有效地进行 code review 是一个循序渐进的过程。如果你所处的角色无法很快改变团队的工作方式，那么可以从把自己的代码发给别人 review 开始，实际可见的价值是最有说服力的。

![img](https://cdn.kelu.org/blog/2019/01/ef9d08f5dca066c34c1748e85494c639_hd.jpg)



# 从CODE REVIEW 谈如何做技术

这两天，在微博上表达了一下Code Review的重要性。因为翻看了阿里内部的Review Board上的记录，从上面发现Code Review做得好的是一些比较偏技术的团队，而偏业务的技术团队基本上没有看到Code Review的记录。当然，这并不能说没有记录他们就没有做Code Review，于是，我就问了一下以前在业务团队做过的同事有没有Code Review，他告诉我不但没有Code Review，而且他认为Code Review没用，因为：

1）工期压得太紧，时间连coding都不够，以上线为目的，

2）需求老变，代码的生命周期太短。所以，写好的代码没有任何意义，烂就烂吧，反正与绩效无关。

我心里非常不认同这样的观点，我觉得我是程序员，我是工程师，就像医生一样，不是把病人医好就好了，还要对病人的长期健康负责。对于常见病，要很快地医好病人很简单，下猛药，大量使用抗生素，好得飞快。但大家都知道，这明显是“饮鸩止渴”、“竭泽而渔”的做法。医生需要有责任心和医德，我也觉得程序员工程师也要有相应的责任心和相应的修养。东西交给我我必需要负责，我觉得这种负责和修养不是”做出来“就了事了，而是要到“做漂亮”这个级别，这就是“山寨”和“工业”的差别。而只以“做出来”为目的标准，我只能以为，这样的做法只不过是“按部就班”的堆砌代码罢了，和劳动密集型的“装配生产线”和“砌砖头”没有什么差别，在这种环境里呆着还不如离开。

老实说，因为去年我在业务团队的时候，我的团队也没有做Code Review，原因是多样的。其中一个重要原因是，我刚来阿里，所以，需要做的是在适应阿里的文化，任何公司都有自己的风格和特点，任何公司的做法都有他的理由和成因，对于我这样的一个初来者，首要的是要适应和观察，不要对团队做太多的改动，跟从、理解和信任是融入的关键。（注：在建北京团队和不要专职的测试人员上我都受到了一些阻力），所以跟着团队走没有玩Code Review。干了一年后，觉得我妥协了很多我以前所坚持的东西，觉得自己的标准在降低，想一想后背拔凉拔凉的，所以我决定坚持，而且还要坚持高标准。

对于Code Review很重要的这个观点，在微博上抛出来后，被一些阿里的工程师，架构师/专家，甚至资深架构师批评，我在和他们回复和讨论的过程中，居然发现有个“因为对方用户的设置”我无法回复了（我被拉黑了，还有一些直接就是冷讽和骂人了，微博中我就直接删除了）。这些批评我的阿里工程师/架构师的观点总结一下如下：（**顺便说一下，阿里内还是有很多团队坚持做Code Review的**）

1）到业务团队体会一下，倒逼工期的项目有多少？订好交付日期后再要求提前1个月的有多少？现在是做到已经不容易，更不谈做得漂亮！。

2）Code Review是一种教条，意义不大，有测试，只要不出错，就可以了。

3）目标都是改进质量，有限的投入总希望能有最大的产出，不同沉湎改进质量的方式不一样，业务应用开发忙的跟狗一样，而且业务逻辑变化快，通用性差，codereviw的成本要比底层高。

4）现在的主要矛盾是倒排出来的工期和不靠谱的程序员之间的矛盾，我认为cr不是解决这个问题的银弹。不从实际情况出发光打正义的嘴炮实在太过于自慰了 。

**我们可以看到，上面观点其实和Code Review没有太多关系，其实是在抱怨另外的问题**。这些观点其实是技术团队和业务团队的矛盾，但不知道为什么强加给了我的“Code Review很重要”的这个观点，然后这些观点反过来冲击“Code Reivew”，并说“Code Review无用”。这种讨论问题的方式在很常见，你说A，我说B，本来A、B是两件事，但就是要混为一谈，然后似是而非的用B来证明你的A观点是错的。（也许，这些工程师/架构师心存怨气，需要一个发泄的通道）

**我觉得，很多时候，人思考问题思考不清楚，很大一部分原因是因为把很多问题混为一谈**，连我自己有些时候都会这样。引以为戒。

即然被混为一谈，那我就来拆分一下，也是下面这三个问题：

- Code Review有没有用的问题。
- Code Review做不起来的问题。
- 业务变化快，速度快的问题，技术疲于跟命。

#### Code Review

你 Google 一下 Code Reivew 这个关键词，你就会发现 Code Review 的好处基本上是不存在争议的，有很多很多的文章和博文都在说Code Review的重要性，怎么做会更好，而且很多公司在面试过程中会加入“Code Review”的问题。打开[Wikipedia的词条](http://zh.wikipedia.org/wiki/%E4%BB%A3%E7%A0%81%E5%AE%A1%E6%9F%A5)你会看到这样的描述——

> 卡珀斯·琼斯（Capers Jones）分析了超过12,000个软件开发项目，其中使用正式代码审查的项目，发现潜在缺陷率约在60-65%之间，若是非正式的代码审查，发现潜在缺陷率不到50%。大部份的测试，发现的潜在缺陷率会在30%左右。
>
> 对于一些关键的软件（例如安全关键系统的嵌入式软件），一般的代码审查速度约是一小时150行程序码，一小时审查数百行程序码的审查速度太快，可能无法找到程序中的问题。代码审查一般可以找到及移除约65%的错误，最高可以到85%。
>
> 也有研究针对代码审查找到的缺陷类型进行分析。代码审查找到的缺陷中，有75%是和计算机安全隐患有关。对于产品生命周期很长的软件公司而言，代码审查是很有效的工具。

**Code Review的好处我觉得不用多说了，主要是让你的代码可以更好的组织起来，有更易读，有更高的维护性，同时可以达到知识共享，找到bug只是其中的副产品**。这个东西已经不新鲜了，你上网可以找到很多文章，我就不多说了。就像你写程序要判断错误一样，Code Review也是最基本的常识性的东西。

我从2002年开始就浸泡在严格的Code Review中，我的个人成长和Code Review有很大的关系，如果我的成长过程中没有经历过Code Review这个事，我完全不敢想像。

**我个人认为代码有这几种级别：1）可编译，2）可运行，3）可测试，4）可读，5）可维护，6）可重用。通过自动化测试的代码只能达到第3）级，而通过Code Review的代码少会在第4）级甚至更高。**关于Code Review，你可以参看本站的《[Code Review中的几个提示](https://coolshell.cn/articles/1302.html)》

可见，Code Review直接关系到了你的工程能力！

#### Code Review 的问题

有下面几个情况会让你的Code Review没有效果。

首当其冲的是——“**人员能力不足**”，我经历过这样的情况，Code Review的过程中，大家大眼瞪小眼，没有什么好的想法，不知道什么是好的代码，什么是不好的代码。导致Code Review大多数都在代码风格上。今天，我告诉你，代码风格这种事，是每个程序员自查的事情，不应该浪费大家的时间。对此，我有两个建议：1）你团队的人招错了，该换血了。2）让你团队的人花时候阅读一下《[代码大全](http://book.douban.com/subject/1477390/)》这本书（当然，还要读很多基础知识的书）。

次当其冲的是——“**结果更重要**”，也就是说，做出来更重要，做漂亮不重要。因为我的KPI和年终奖based on how many works I’ve done！而不是How perfect they are ! 这让我想到那些天天在用Spring MVC 做CRUD网页的工程师，我承认，他们很熟练。大量的重复劳动。其实，仔细想一下好多东西是可以框架化，模板化，或是自动生成的。所以，为了堆出这么多网页就停地去堆，做的东西是很多，但是没有任何成长。急功近利，也许，你做得多，拿到了不错的年终奖，但是你失去的也多，失去了成为一个卓越工程师的机会。你本来可以让你的月薪在1-2年后翻1-2倍的，但一年后你只拿到了为数不多的年终奖。

然后是——“**人员的态度问题**”，一方面就是懒，不想精益求精，只要干完活交差了事。对此，你更要大力开展Code Review了，让这种人写出来的代码曝光在更多人面前，让他为质量不好的代码蒙羞。另一方面，有人会觉得那是别人的模块，我不懂，也没时间 去懂，不懂他的业务怎么做Code Review? 我只想说，如果你的团队里这样的“各个自扫门前雪”的事越多，那么这个团队也就越没主动性，没有主动性也就越不可能是个好团队，做的东西也不可能好。而对于个人来说，也就越不可能有成长。

接下来是——“**需求变化的问题**”，有人认识，需求变得快，代码的生存周期比较短，不需要好的代码，反正过两天这些代码就会被废弃了。如果是一次性的东西，的确质量不需要太高，反正用了就扔。但是，我觉得多多少少要Review一下这个一次性的烂代码不会影响那些长期在用的代码吧，如果你的项目全部都是临时代码，那么你团队是不是也是一个临时团队？关于如果应对需求变化，你可以看看本站的《[需求变化与IoC](https://coolshell.cn/articles/6950.html)》《[Unix的设计思想来应对多变的需求](https://coolshell.cn/articles/7236.html)》的文章 ，从这些文章中，我相信你可以看到对于需求变化的代码质量需要的更高。

最后是——“**时间不够问题**”，如果是业务逼得紧，让你疲于奔命，那么这不是Code Review好不好问题，这是需求管理和项目管理的问题以及别的非技术的问题。下面我会说。

不管怎么样，上述Code Review的问题不应该成为“Code Review无意义”的理由或借口，这就好像“因噎废食”一样。干什么事都会有困难和问题的，有的人就这样退缩了，但有的人看得到利大于弊，还是去坚持，人与人的不同正在这个地方。这就是为什么运动会受伤，但还是会人去运动，而有人因为怕受伤就退缩了一样。

#### 被业务逼得太紧

被业务逼得太紧，需求乱变，这其实和Code Review没有多大关系了。对此，我想先讲一个我的故事。

我去年在阿里的聚石塔，刚去的时候，聚石塔正在做一个很大的重构——对架构的大调整。因此压了很多业务需求，等这个项目花了2-3个月做完了后，一下子涌入了30-50个需求，还规定一个月完成，搞得团队疲于奔命。在累了两周后，我仔细分析了一下这些需求，发现很多需求是在重复做阿里云已经做过的东西，还有一些需求是因为聚石塔这个平台不规范没有标准所产生的问题。于是，我做了这么三件事：

1）重新定义聚石塔这个产品主要目标和范围，确定哪些该做，哪些不该做。

2）为聚石塔制定标准 ，让阿里云的API都长得基本一样，并制订云资源的接入标准。

3）推动重构阿里云的Portal系统，不再实现阿里云已经做过的东西，与阿里云紧密结合。

这些事情推动起来并不容易，聚石塔的业务方一开始也不理解，我和产品一起做业务方的工作，而阿里云也被我逼得很惨（在这里一并感谢，尤其阿里云的同学，老实说，和阿里云跨团队合作中是我这么多年来感觉最好的一次，相当赞）。通过这个事，聚石塔需求一下就有质的下降了。搞得还有几个工程师来和我说，你这么搞，聚石塔就没事可干了。姑且不说工程师对聚石塔的理解是怎么样的。 我只想说，我大量地减少了需求，尽最大可能联合了该联合的人，而不是自己闭门造车，并让产品的目标和方向更明确了。做了这些事情后，大家不但不用加班，而且还有时间充电去学技术，并为聚石塔思考未来的方向和发展。去年公司996的时候，我的团队还在965（搞得跟异教徒似的），而且还有很多时间去专研新的东西。

说这个故事，我不是为了得瑟，而是因为有些人在微博上抨击我是一个道貌岸然的只会谈概念讲道理的装逼犯。所以，我告诉大家我在聚石塔是怎么做的，我公开写在这里，你也可以向相关的同学去求证我说的是不是真的。也向你证明，我可能是个装逼犯，但绝不是只会谈概念讲道理的装逼犯。

被业务方逼得紧不要抱怨，你没有时间被逼得像牲口一样工作，这个时候，你需要的是暂停一下想一想，为什么会像牲口一样？而这正是让你变得聪明的机会。

我为你总结一下，

1）你有没有去Review业务部门给你的这么多的需求，哪些是合理的，哪些是不合理的。在Amazon，开发工程师都会被教育拿到需求后一定要问——“为什么要做？业务影响度有多大？有多少用户受益？”，回答不清这个问题，没有数据的支持，就不做。所以，产品经理要做很多数据挖拙和用户调研的工作，而不是拍拍脑袋，听极少数的用户抱怨就要开需求了。

2）产品经理也要管理和教育的。你要告诉你的产品经理：“你是一个好的产品经理，因为你不但对用户把握得很好，也会对软件工艺把握得很好。你不但会开出外在的功能性需求，也同样会开出内在的让软件系统更完善的非功能性需求。你不是在迁就用户，而是引导用户。你不会无限制地加功能，而是把握产品灵魂控制并简化功能。你会为自己要做的和不做东西的感到同样的自豪。”你要告诉你的产品经理：“做一个半成品不如做好半年产品”（更多这样的观点请参看《[Rework摘录和感想](https://coolshell.cn/articles/9156.html)》）

3）做事情是要讲效率的。Amazon里喜欢使用一种叫T-Shirt Size Estimation的评估方法来优先做投入小产出大的“Happy Case”。关于什么是效率，什么是T-Shirt Size Estimation，你可以看看《[加班与效率](https://coolshell.cn/articles/10217.html)》一文 。

4）需求总是会变化的，不要抱怨需求变化太快。你应该抱怨的是为什么我们没有把握好方向？老变？这个事就像踢足球一样，你要去的地方是球将要去的地方，而不是球现在的地方。你要知道球要去哪里，你就知道球之前是怎么动的，找到了运动轨迹后，你才知道球要去像何方。如果你都不知道球要去向何方，那你就是一只无头苍蝇一样，东一下西一下。

**当你忙得跟牲口一样，你应该停下来，问一下自己，自己成为牲口的原因，是不是就是因为自己做事时候像就牲口一样思考？**

#### 其它

最后，我在给阿里今年新入职的毕业生的“技塑人生”的分享中，我给他们布置了5、6个Homework，分享几个给大家：

1）重构或写一个模块，把他做成真正的Elegant级别。

2）与大家分享一篇或几篇技术文章 ，并收获10-30个赞。

3）降低现有至少20%的重复工作或维护工作

4）拒绝或简化一个需求（需要项目中所有的Stakeholders都同意）

部署这些作业的原因，是我希望新入行的同学们对自己的工作坚持高的标准，我知道你们会因为骨感的现实而妥协，但是我希望你们就算在现实中妥协了也要在内心中坚持尽可能高的标准，不要习惯成自然，最后被社会这个大染缸给潜移默化了。因为你至少要对自己负责。**对自己负责就是，用脚投票，如果妥协得受不了了就离开吧**。