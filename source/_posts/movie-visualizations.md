title: 和电影有关的可视化作品
date: 2013-12-16 01:45:22
tags: dataviz
---
电影电视是一种最具表现力的媒介，对其进行数据挖掘和可视化分析的作品同样多姿多彩，可以是基于文本的（叙事、人物关系、台词），基于视听的（色彩、音响、动作、剪辑），还有基于创作者的（导演、演员、编剧），基于观众反馈的（票房、口碑），甚至直接用数据可视化作为影片内容。笔者收集整理一些不错的影视可视化作品，介绍给大家。
<!--more-->

##	TL;DR

### 影视文本内容分析

{% blockquote %}
Visualizing 500 Days of Summer
http://rasagy.github.io/500days/
作者：Rasagy Sharma
{% endblockquote %}

介绍：《和莎莫的500天》是一部非线性叙事的爱情喜剧，设计师Rasagy Sharma抽取出影片中男女主人公关系的变化，并用可视化手段再现了这一有趣的叙事模型。

他收集整理出的结构化数据包括：场景编号, 开始&结束时间, 场景时长, 天数编号, 有趣台词, 场景介绍, 场景地点。

动画图例说明：气泡和弧线出现顺序完全按照影片叙事顺序，气泡大小为场景时长，气泡颜色为人物三种关系（在一起、分开、偶遇），点击气泡还能查看一句最有趣的台词引用。

制作工具为D3.js，实际上是气泡图（三个数值）+弧线路径的综合运用。作者blog里对整个制作过程进行了详细的描述，有兴趣可以深入阅读。

{% blockquote %}
Rocky Morphology
http://fathom.info/rocky/
作者：Fathom.info
{% endblockquote %}

介绍：史泰龙新片热映之际，洛基也即将登录百老汇舞台，Fathom团队的成员推出一部很棒的可视化作品，展现洛基系列中的关键叙事元素。分析方法参考自前苏联民俗学和语言学家普罗普的故事形态学理论，洛基的传奇故事十分符合普罗普提出的民间故事中“功能”的概念，于是Fathom团队从影片中提取出6个基本功能：对话、训练、蒙太奇（闪回）、预战斗、战斗、演职员表。

通过对几种功能在每一部影片中出现的时间、时长的可视化，可以明显看出每部影片叙事特点：

6部洛基都是以一段战斗开始（红色），前2部洛基叙事非常线性，用冗长的对话来进行铺垫，直到影片2/3处才开始一大段训练，接着闪回、预战斗，最后在战斗中结束影片。

洛基3的叙事则有了明显的改变，片头的打斗吸引观众之后引入一段蒙太奇闪回，整部影片不断穿插一些小的战斗和训练，在影片高潮迎来最终之战。

{% blockquote %}
Dissecting a Trailer: The Parts of the Film That Make the Cut
http://www.nytimes.com/interactive/2013/02/19/movies/awardsseason/oscar-trailers.html
作者：SHAN CARTER, AMANDA COX, MIKE BOSTOCK @ NYTimes
{% endblockquote %}

介绍：2013年奥斯卡奖颁奖之前，纽约时报对5部获得最佳影片提名电影的预告片进行了可视化分析。通过对比预告片与整片镜头的位置、时长，来观察每部电影是如何用预告片来推销自己的：

有的遵循了标准的预告片模式，依次介绍主要角色，基本保持与整片同步的叙事顺序。比如《乌云背后的幸福线》。

有的则更像是预热的广告片，不像预告片那样专注在角色上，而是营造出整个影片的氛围，吊人胃口。比如《林肯》。

作为唯一一部提名的外国电影，《爱》的预告片每个镜头都更长，甚至大胆地在最后使用了20秒的老人静坐画面，这种安静和未知充满张力。

《逃离德黑兰》综合了两种调性：惊悚和好莱坞式的讽刺，惊悚意味着更快的剪辑切换，但轮到讽刺时镜头会稍长。

《南国野兽》的预告片中呈现出一种世界的“诗意”，结束时留下一个开放性的问题，给人想象和讨论的空间，保持影片的神秘野性。

这个可视化作品非常简洁，是D3基本图表的进阶运用。时间轴的横轴是预告片时间线，纵轴是素材在原片位置，bar的宽度代表时长，鼠标滑过每一个数值，右上角预告片切换至相应的定格画面。


{% blockquote %}
Mad Drinks
http://www.maddrinkers.com/
作者：Arianna Belotti, Sofia Girelli, Daniele Lupatini, Gianluca Malimpensa, Mattia Parietti, Aurelie Pellat
{% endblockquote %}


介绍：艾美奖金球奖双料得主《广告狂人》展现了二十世纪六十年代大都会的浮夸与复杂人性，剧中充斥着香烟、烈酒和性场面。来自意大利的一个小组收集了第一季中人物角色的这些“坏行为”：时间、地点、主要人物关系、饮酒和吸烟行为，并特别为酒类添加了详细信息，以此制作了5幅信息图。所有的数据收集处理和呈现一共花了5天的时间。从图上可以看出，第7集角色们喝得最多也抽得最多。

{% blockquote %}
Previously, On Arrested Development
http://apps.npr.org/arrested-development/
作者：Jeremy Bowers, Adam Cole, Danny DeBelius, Christopher Groskopf and Alyson Hurt @NPR
{% endblockquote %}

介绍：风靡一时的喜剧《发展受阻》被砍7年之后，第四季在Netflix上回归。《发展受阻》拥有不少死忠粉丝的原因在于，其每集笑料经常来源于上一两集埋下的包袱，这种无处不在的互文性，吸引了资深喜剧迷的持续关注。（同样对该剧着迷的）NPR的数据新闻团队在新剧回归之前，把前三季中每个角色具有重复性和关联性的笑料，用可视化的手段展现了出来。新剧开播之后NPR持续更新了新一季的笑料。

{% blockquote %}
Where have all the wildlings gone?
http://www.wherehaveallthewildlingsgone.com/
作者：Nigel Evan Dennis
{% endblockquote %}

介绍：设计师Nigel Evan Dennis为他热爱的史诗奇幻剧《冰与火之歌 权力的游戏》设计制作了一个站点，重新解析了剧中的场景、人物、地图、时间线、道具和重要概念。

{% blockquote %}
ALL IN THE FAMILY TREE
http://fathom.info/allinthefamilytree/
作者：Fathom.info
{% endblockquote %}

介绍：同样来自Fathom成员的作品，为70年代经典肥皂剧ALL IN THE FAMILY及其7部衍生剧中所有的人物角色制作了一个家族树。每一个角色都以一片树叶来呈现，相同颜色的代表同一部剧。一条分支线连接了同一个角色在原生剧和衍生剧中的关系。

{% blockquote %}
Moviegalaxies
http://moviegalaxies.com/
作者：Jermain Kaminski, Michael Schober
{% endblockquote %}

介绍：Moviegalaxies是一个电影角色关系可视化搜索和展示的网站，输入影片名称或者影人，可以搜索到相关电影中角色之间的关系网络，快速查看到主要人物、人物之间如何关联。Moviegalaxies用三个指标来显示人物之间的关联度：

中心性：betweenness，一个人物在一个连接上的重要性；

关系度：degree，一个人物会有多少个连接；

群组数：cluster，一个人物的关系网络有多少分支。

根据人物出现场景、共同对话、对话频次，通过一定的算法计算出得出这些指标，可以参考Social Network Analysis相关论文。绘图工具则是基于Sigma.js这个开源图形库。

{% blockquote %}
Geography, class, and fate: Passengers on the Titanic
http://storymaps.esri.com/stories/titanic/
作者：ESRI地图公司
{% endblockquote %}

介绍：该作品并不是对电影的直接分析，地图服务商ESRI根据维基百科中泰坦尼克乘客的真实情况制作了一幅地图，还原当时这艘巨船上不同舱位乘客的家乡、登船点、目的地、幸存情况等信息。比如影片中那对相拥等死的Straus夫妇。

###	影视视听语言分析

{% blockquote %}
CINEMETRICS
http://cinemetrics.fredericbrodbeck.de/
作者：Frederic Brodbeck
{% endblockquote %}

介绍：德国设计师Frederic Brodbeck令人惊艳的毕业作品，从试听语言的角度完全重构了数部经典电影。Brodbeck用Python开发了一个复杂的工具来完成电影数据提取分析工作，把光影配色、剪辑结构、动作模式、台词频率这些元素，按时间顺序组成一个圆环，每一个圆环就像影片的指纹一样，揭示出影片的影调、节奏，从中你能直观感受不同类型片的风格差异，也能观察到同一导演的风格痕迹。

比如：动画片《汤普森大电影》的圆环呈现出五彩斑斓的颜色，《黑客帝国》则是标志性的暗绿色。动作片《007：大破量子危机》的圆环边缘起起伏伏，科幻片《2001：太空漫游》则非常平滑。

作者在主页上大致介绍了项目制作方法：

原始数据的处理：从DVD抓取视频、音频、字幕、章节数据，从IMDB抓取台词引用。

抽取的电影数据：镜头数、平均镜头长度、动态画面测量（相对于静止画面来说）、光影配色。

其中配色的算法：每部影片、每个章节、每个镜头甚至每一帧都可以被分为5种配色，然后组成该影片的色盘。

更多的信息可以购买作者本人写的一本书，深入探讨了项目每个阶段的设想和实现。


{% blockquote %}
Distribution of colours in movie posters between 1914 and 2012
http://www.vijayp.ca/movies/new_page.html
作者：Vijay Pandurangan
{% endblockquote %}

介绍：同样是用Python进行色彩分析，Vijay Pandurangan的研究对象是1914年以来的电影海报配色。Pandurangan是怎么用可视化来揭示这些海报配色的特点呢？

首先，忽略掉黑白两色，每个年份是一条水平的色彩条（采用的HSL颜色系统）。

其次，每种色调的宽度代表该年所有海报中出现这种色调的数量，饱和度和亮度则代表所有符合这种平均色系的像素。这样就能看出每年用得最多的海报色是橘红色。

再次，按照年份依次列出每年的色彩条，从上到下观察，你会发现近年来蓝色系的海报变得多了起来。

然后，作者还设计了一套通用颜色系统下的色彩条（忽略掉饱和度、亮度），你会更加直观地观察到色彩的变化。

最后，点击每个色彩条，你能进一步查看影片海报色分布的饼图。

作者blog对可视化方法也进行了详细的描述，有兴趣的可以深入阅读。

下面两个作品也是利用Python，对整部影片进行色彩抽取压缩，形成色彩“条形码”。Movie Barcode是只生成一张图片，而Film Strips在此基础上给出了每个色彩对应的影片截图。

{% blockquote %}
Movie Barcode
http://moviebarcode.tumblr.com/

Film Strips
http://roadtolarissa.com/film-strips/
作者：Adam Pearce
{% endblockquote %}

###	影人和影片口碑分析

{% blockquote %}
Constellations of Directors and Their Stars
http://www.nytimes.com/newsgraphics/2013/09/07/director-star-chart/
作者：MIKE BOSTOCK, JENNIFER DANIEL, ALICIA DESANTIS and NICOLAS RAPOLD @NYTimes
{% endblockquote %}

介绍：D3的创造者MIKE BOSTOCK加入纽约时报之后做了很多有意思的作品，比如这个项目：电影导演和他们的御用演员，展示了20世纪30年代到2010年代期间，一些知名导演与他们的御用演员之间的合作关系，形成一个个星座图。

演员选取的标准是与导演至少合作过4部电影。让我们看看有哪些模式：

一个导演只与一个演员保持长期合作，他们之间星座图是一个简单的菱形。比如斯皮尔伯格与哈里森·福特。

一个导演与多个演员长期合作，例如王家卫与梁朝伟、张曼玉，韦斯·安德森与他的“黄金三角”威尔逊兄弟和比尔·莫瑞。他们之间的星座图是多角菱形。

有些演员同时和两位导演保持长期合作关系，于是两个星座连接在了一起。例如处于科波拉和伍迪·艾伦之间的黛安·基顿。有趣的是伍迪·艾伦有四位爱将，他们之间却没有合作关联。

还有一些多产的导演频繁与许多演员保持长期的合作，这些演员之间的合作也相当交错，于是整个星座出现杂乱如麻的形状。例如约翰·福特和黑泽明和他们数量庞大的演员阵容。

{% blockquote %}
The Social Oscars
http://labs.brandwatch.com/oscars/
作者：Brandwatch公司
{% endblockquote %}

介绍：著名设计公司Brandwatch对2013年奥斯卡各个奖项的口碑分析，包括影评人、公众的不同评价和预测。

###	可视化作为影片内容

{% blockquote %}
Bear 71
http://bear71.nfb.ca/#/bear71
作者：National Film Board of Canada
{% endblockquote %}

介绍：从2001-2009年之间，加拿大野生动物保护员跟踪记录了一头雌性灰熊的真实足迹，结合可视化地图制作成一部影片，展示这只灰熊生活的历程。

*该文首发于：[数据新闻网](http://djchina.org/2013/12/13/visualizing_movies/)*