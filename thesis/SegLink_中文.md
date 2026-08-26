# SegLink论文中文版

## 摘要

大多数最先进的文本检测方法都是特定的水平拉丁语文本，在实时应用中速度不够快。我们介绍Segment Linking（SegLink），一种带方向的文本检测方法。其主要思想是将文本分解为两个局部可检测的元素，称之为segments和links。Segment是一个带方向的框，覆盖单词或文本行的一部分；Link两个相邻的segment，表示它们属于同一个单词或文本行。通过端到端训练的全卷积神经网络在多个尺度上密集地检测这两个元素。最后的检测是通过组合links连接的segments来产生的。与以前的方法相比，SegLink在精度方面有所提高，速度快，训练容易。它在标准ICDAR 2015 Incidental (Challenge 4)  基准上实现了75.0%的f指标，以较大幅度超越了之前的最佳水平。它在512×512个图像上以超过20 FPS的速度运行。而且，SegLink不需要修改就可以检测到非拉丁语文本行，如中文。

## 1. 介绍

阅读自然图像中的文本是一个具有挑战性的课题。它由许多实际应用驱动，如照片OCR[2]、地理位置和图像检索[9]。在文本阅读系统中，文本检测通常是具有重要意义的第一步。从某种意义上说，文本检测可以看作是应用于文本的对象检测，其中文字/字符/文本行作为检测目标。因此，最近出现了一种新的趋势，即最先进的文本检测方法[9，6，22，30]主要基于先进的通用对象检测或分割技术，例如[4，5，15]。

![SegLink_图1](img/SegLink_图1.png)

<center><font size=2>图1 SegLink概览。上面一行显示图像有两个不同尺度和方向的词。（a）分段（黄色框）在图像上检测到。（b）链接（绿线）在相邻段对之间检测到。（c）分段通过链接连接的词被组合成一个整体。（d-f）SegLink公司能够检测到拉丁语和非拉丁语文本的长行，例如中文。</font></center>
尽管前面的工作取得了很大的成功，但我们认为，由于两个主要原因，一般的检测方法不太适合文本检测。首先，文字/文本行边界框的宽高比一般对象的宽高比要大得多。（fast/faster ）R-CNN[5、4、19]-或SSD[14]型探测器可能由于其方案或Anchor box设计而难以生产此边框。此外，一些非拉丁语文本的单词之间没有空格，因此边界框的纵横比更大，这使得问题更加严重。其次，不同于一般的对象，文本通常有一个清晰的边界和方向[25]。对于文本检测器来说，生成定向框是很重要的。然而，大多数通用的对象检测方法并不是为了产生定向框而设计的。

为了克服上述挑战，我们从一个新的角度来解决文本检测问题。我们建议将长文本分解为两个较小的和局部可检测的元素，即segment和link。如图1所示，segment是覆盖一个词的一部分的定向框（为了清楚起见，我们在这里和以后使用“词”，但segment也可以无缝地在包含多个词的文本行上工作）；Link连接一对相邻的segment，表示它们属于同一个词。在上述定义下，一个单词由若干个segment以及它们之间链接来进行定位。在检测过程中，利用卷积神经网络对输入图像进行密集检测。然后，根据link将segment组合成完整的单词。

这种方法的主要优点是，由于两个基本元素都是本地可检测的，所以现在可以在本地检测到长且有方向的文本：检测一个segment不需要观察整个单词。也没有链接，因为两个segment的连接可以从本地上下文推断出来。此后，我们可以检测任意长度和方向的文本，具有极大的灵活性和效率。

具体地说，我们提出了一个卷积神经网络（CNN）模型，以完全卷积的方式同时检测segment和link。网络采用VGG-16[21]作为骨干网。添加了一些额外的特征层。在6个特征层中加入卷积预测器来检测不同尺度下的segment和link。为了解决冗余检测问题，我们引入了两种类型的link，即层内link和跨层link。层内link将segment连接到同一层上的相邻段。另一方面，跨层link将一个segment连接到较低层上的相邻segment。通过这种方式，我们连接相邻位置的segment以及比例。最后，我们使用深度优先搜索（DFS）算法找到经过连接的segment，并将它们组合成整词。

我们的主要贡献是提出了一种新的分段连接检测方法。通过实验，我们证明了该方法与其他最新方法相比具有几个显著的优点：1）稳健性：SegLink以简单优雅的方式对有向文本的结构进行建模，具有对复杂背景的稳健性。我们的方法在标准数据集上取得了非常有竞争力的结果。特别是，在ICDAR 2015 Incidental (Challenge 4)  基准[12]上，它在f-measure （75.0% vs 64.8%）方面的表现大大超过了之前的最佳水平；2）效率：SegLink由于其单通、完全卷积的设计而具有很高的效率。它每秒处理超过20幅512x512大小的图像；3）通用性：SegLink无需修改即可检测出中文等非拉丁文本的长行。我们在一个多语言数据集上演示了这种能力。

## 2. 相关工作

在过去的几年中，人们对文本检测问题进行了大量的研究[24，23，17，17，25，7，8，30，29，2，9，6，22，26]。基于基本的检测目标，以往的方法大致可以分为三类：基于字符的、基于词的和基于行的。基于字符的方法[17，23，24，10，7，8]检测单个字符并将其分组成单词，这些方法通过对区域提取算法提取的候选区域进行分类或对滑动窗口进行分类来查找字符。这种方法通常涉及将字符分组为单词的后处理步骤。基于词的方法[9，6]直接检测词的边界框。它们通常与最近基于CNN的通用目标检测网络有类似的管道。这些方法虽然具有很好的检测精度，但如前所述，当应用于中文等非拉丁语文本时，性能可能会下降。基于行的方法[29，30，26]使用一些图像分割算法来查找文本区域。它们还需要一个复杂的后处理步骤，即单词分割和/或FP(原文false positive  )删除。与以前的方法相比，我们的方法在一个前向网络中联合预测segment和link。这条管道简单而清洁。此外，网络是端到端可训练的。

文本检测可以看作是一般目标检测的一个特例，是计算机视觉中的一个基本问题。大多数最先进的检测系统要么使用CNN[5，4，19]对一些类不可知的对象建议进行分类，要么直接从一组预设框（例如锚定框）中回归对象边界框[18，14]。我们的网络结构继承了SSD[14]的结构，SSD[14]是一种最新的目标检测模型。SSD提出了利用卷积预测器在多特征层上检测目标的思想。我们的模型还以非常相似的方式检测片segment和link。尽管模型相似，我们的检测策略却有很大的不同：SSD直接输出对象边界框。另一方面，我们采用自下而上的方法，检测单词或文本行的两个组成元素，并将它们组合在一起。

## 3. Segment Linking 

我们的方法用一个前馈CNN模型来检测文本。在给定$w_I×h_I$大小的输入图像I的情况下，该模型输出固定数量的片segment和link，然后根据它们的置信度对其进行过滤，并将其组合成整个单词边界框。边框是一个旋转的矩形，用$b=（x_b，y_b，w_b，h_b，θ_b）$表示，其中$x_b，y_b$是中心的坐标，$w_b，h_b$是宽度和高度，$θ_b$是旋转角度。

### 3.1 CNN模型

图2示出了网络架构。我们的网络使用预先训练的VGG-16网络[21]作为主干（conv1到pool5）。之后[14]，VGG-16的全连接层被替换为卷积层（fc6替换为conv6；fc7替换为conv7）。接着是一些额外的卷积层（conv8_1到conv11），它们用更大的感受野提取更深层的特征。它们的结构如图2所示。

![SegLink网络结构](img/SegLink网络结构.png)

<center><font size=2>图2 网络架构。该网络由卷积特征层（显示为灰色块）和卷积预测器（细灰色箭头）组成。卷积滤波器以“（#滤波器）、k（内核大小）s（步长）”的格式指定。多行过滤器规范意味着之间有一个隐藏层。分段（黄色框）和链接（不显示）由多个特征层上的卷积预测器检测（由l=1...6） 并通过一种组合算法组合成整词。</font></center>
在6个特征层上检测到segment和link，分别是conv4_3、conv7、conv8_2、conv9_2、conv10_2和conv11。这些特征层提供不同粒度的高质量深层特征（conv4_3最细，conv11最粗）。在6层中每层增加一个3×3核的卷积预测器来检测segment和link。我们将特征层和预测器索引为l=1......6。

Segment检测。Segment也是定向框，用$s=（x_s，y_s，w_s，h_s，θ_s）$表示。我们通过估计输入图像上一组默认框[14]的置信分数和几何偏移来检测片段。每个默认框都与一个特征图位置相关联，其分数和偏移量将根据该位置的特征进行预测。为了简单起见，我们只将一个默认框与特征图位置相关联。

考虑特征映射大小为$w_l×h_l$的第 $l$ 特征层。此特征图上的位置（x，y）对应于图像上以$（x _a，y_a）$为中心的默认框，其中：

![SegLink_公式1](img/SegLink_公式1.png)

默认框的宽度和高度都设置为常数$a_l$。

卷积预测器产生7个通道用于segment检测。其中，对2个通道进行进一步softmax-normalized 得到（0，1）中的分段分数。其余5个是几何偏移。考虑到图上的一个位置（x，y），我们表示这个位置的向量沿深度方向$(\Delta x_s，\Delta y_s，\Delta w_s，\Delta h_s，\Delta θ_s)$。然后，在此位置的segment通过以下公式计算：

![SegLink_公式2-6](img/SegLink_公式2-6.png)

这里，常数$a_l$控制输出段的比例。它的选择应该考虑到第l层的感受野大小。我们用经验公式选择这个尺寸：$a_l=γ\frac{w_I}{w_l}$，其中$γ=1.5$。

**层内Link检测**。Link连接一对相邻的segment，表示它们属于同一个单词。这里，相邻的segment是在相邻的特征图位置检测到的segment。Link不仅是将segment组合成完整单词所必需的，而且有助于分隔两个相邻单词-在两个相邻单词之间，segment应该被预测为否定的。

![SegLink_图3](img/SegLink_图3.png)

<center><font size=2>图3 层内和跨层link。（a）conv8_2上的一个位置（黄色块）及其8个连接的邻居（带或不带填充的蓝色块）。检测到的层内链接（绿线）将同一层上的一个段（黄色框）与其相邻的两个段（蓝色框）连接起来。（b） 跨层link连接conv9_2上的一个段（黄色框）和conv8 2上的两个段（蓝色框）。</font></center>
我们使用相同的特征来显式地检测segment之间的link。由于我们在一个特征图位置只检测到一个segment，因此segment可以通过其图位置（x，y）和图索引l，表示为$s^{（x，y，l)}$。如图3.a所示，我们定义在同一特征层上，一个段与其8个相连的相邻段在层内：

![SegLink_公式7](img/SegLink_公式7.png)

当局部检测到segment时，输入图像上的一对相邻segment也相邻。卷积预测器也能检测到link。预测器为8个连接的相邻segment的link输出16个信道。每2个通道都是softmax-normalized 的，以获得link的分数。

**跨层link检测**。在我们的网络中，在不同的特征层上检测不同尺度的segment。每个层处理一系列比例。我们使这些范围重叠，以便不错过在其边缘的比例。但结果是，同一个单词的segment可以同时在多个层上被检测到，从而产生冗余。

为了解决这个问题，我们进一步提出了另一种类型的link，称为跨层link。跨层link使用相邻索引连接两个特征图层上的segment。例如，在conv4_3和conv7之间检测到跨层link，因为它们的索引分别为l=1和l=2。

这一对的一个重要特性是，由于它们之间的下采样层（max pooling或stride-2卷积），第一层的大小总是第二层的两倍。请注意，只有当所有特征图层的大小都为偶数时，此特性才有效。在实际应用中，我们通过将输入图像的宽度和高度都可分割128来确保这一特性。例如，1000×800图像的大小调整为1024×768，这是最接近的有效大小。如图3.b所示，我们将段的跨层邻居定义为：

![SegLink_公式8](img/SegLink_公式8.png)

它们是前一层的片段。每段有4个跨层邻居。通过两层之间的双尺寸关系来保证对应关系。

再次，通过卷积预测器检测跨层link。预测器为跨层link输出8个通道。每2个通道都是softmax标准化的，以产生跨层link的分数。在特征层l=2…6上检测到跨层link，但在l=1（conv4_3）上检测不到跨层link，因为它没有进位特征层。

通过跨层link，可以连接不同比例的segment，然后进行组合。与传统的非最大值抑制相比，跨层连接提供了一种可训练的冗余连接方式。此外，它与我们的Link策略完美契合，并且易于在我们的框架下实现。

![SegLink_图4](img/SegLink_图4.png)

<center><font size=2>图4 卷积预测器的输出通道。图块显示深度为31的wl×hl图。l=1的预测器不输出corss层链路的信道。</font></center>
**卷积预测器的输出。**综合起来，图4显示了卷积预测器的输出通道。预测器由卷积层和分别对segment和link得分进行标准化的softmax层实现。此后，我们网络中的所有层都是卷积层。我们的网络是全卷积的	。

### 3.2 合并 Segments 和 Links

在feed转发之后，网络会生成许多segment和link（数量取决于图像大小）。在组合之前，输出segment和link根据它们的置信度得分进行过滤。我们分别为segment和link设置了不同的滤波阈值α和β。从经验上看，我们的模型的性能对这些阈值不是很敏感。两个阈值与它们的最佳值之间的偏差为0.1会导致f-measure下降小于1%。

以过滤后的segment为节点，过滤后的link为边，在其上构造一个图。然后，对图执行深度优先搜索（DFS）以查找其连接的组件。每个组件都包含一组通过link连接的segment。用B表示一个连接的组件，该组件中的segment按照算法1中的步骤组合。

![SegLink_算法1](img/SegLink_算法1.png)

## 4. 训练

### 4.1 Segments和Links真实值 

该网络是由真实的segment和link进行监督训练。真实样本包括所有默认框的标签（即其对应段的标签）、它们到默认框的偏移量以及所有层内和跨层link的标签。我们从这是值的词边界框计算它们。

首先，我们假设在输入图像上只有一个真实词。当前仅当满足以下条件时，该默认框被标记为正向：1）框的中心位于单词边界框内；2）框大小$a_l$和单词高度h之间的比率满足：

![SegLink_公式9](img/SegLink_公式9.png)

否则，默认框标记为反向。

接下来，我们考虑多个单词的情况。如果默认框不符合上述任何单词的条件，则将其标记为反向。否则，将其标记为正向，并与具有最接近大小的单词匹配，即在等式9的左侧具有最小值的单词。

![SegLink_图5](img/SegLink_图5.png)

<center><font size=2>图5 给定一个默认框和一个文字边界框，计算一个真实segment的步骤。</font></center>
偏移量在正默认框上计算。首先，我们按照图5所示的步骤计算真实segment。然后，我们将方程2解为方程6，得到真实segment偏移量。当且仅当满足以下条件时，link（层内或跨层）标记为正向：1）连接到它的两个默认框都标记为正；2）两个默认框与同一个单词匹配。

### 4.2 优化

目标。我们的网络模型通过同时最小化segment分类、偏移回归和link分类的损失来训练。总的来说，损失函数是三个损失的加权和：

![](img/SegLink_公式10.png)

这里，$y_s$是所有segment的标签。如果第i个默认框标记为正，则$y_s（i）=1$，否则为0。同样，$y_l$是链接的标签。$L_{conf}$是预测segment和link得分上的最大softmax损失，分别为$c_s$和$c_l$。$L_{loc}$是预测segment几何参数$\hat{s}$和真实值s上的平滑L1回归损失[4]。Segment类和回归损失用$N_s$进行规范化，$N_s$是正向默认框数。Link分类的损失通过正向link数$N_l$进行规范化。在实际中，重量常数λ1和λ2都被设置为1。

**Online Hard Negative Mining **(不知道这句怎么翻译)。对于segment和link，负面的占据了大部分训练样本。因此，Hard Negative Mining是平衡正负样本的必要条件。我们遵循文献[20]中提出的Online Hard Negative Mining策略，将正负比控制在3:1以内。对片segment和link分别执行Hard Negative Mining。

**数据增强**。我们采用类似于SSD[14]和YOLO[18]的在线增强流水线，将训练图像随机裁剪成一个与任何groundtruth word Crops重叠最小的Jaccard块，并将其大小调整为相同，然后再进行批量加载。对于有向文本，将在词的轴对齐边框上执行增强。对于每个样本，重叠o从0（无约束）、0.1、0.3、0.5、0.7和0.9中随机选择。裁剪大小是从原始图像大小的[0.1，1]中随机选择的。训练图像不会水平翻转。

## 5. 实验

在本节中，我们使用三个公共数据集的标准评估协议，对提议的方法进行评估，即ICDAR 2015 Incidental Text (Challenge 4) 、MSRA-TD500和ICDAR 2013。

### 5.1 数据集

SynthText in the Wild（SynthText）[6]包含800000个合成训练图像。它们是通过将自然图像与使用随机字体、大小、方向和颜色渲染的文本混合而创建的。文本被渲染并与精心选择的图像区域对齐，以便具有逼真的外观。数据集为字符、单词和文本行提供非常详细的注释。我们只使用数据集对我们的网络进行预训练。

ICDAR 2015 Incidental Text (Challenge 4) [12]是ICDAR 2015 Robust Reading Competition 的挑战4。这个挑战的特点是谷歌眼镜拍摄的附带场景文本图像，而不考虑定位、图像质量和视点。因此，数据集在文本方向、比例和分辨率方面表现出很大的变化，这使得它比以前的ICDAR挑战更加困难。数据集包含1000个训练图像和500个测试图像。注释作为单词四边形提供。

MSRA-TD500（TD500）[25]是第一个关注面向文本的标准数据集。数据集也是多语言的，包括中文和英文文本。数据集由300幅训练图像和200幅测试图像组成。与IC15不同，TD500是在文本行级别进行注释的。

ICDAR 2013（IC13）[13]主要包含水平文本，有些文本略有方向。数据集已经被广泛应用于文本检测方法的评价。它由229幅训练图像和233幅测试图像组成。

### 5.2 实现细节

我们的网络在SynthText上进行了预先训练，并在真实数据集（稍后指定）上进行了微调。采用标准SGD算法对其进行优化，动量为0.9。对于预训练和微调，随机裁剪后图像大小调整为384×384。由于我们的模型是完全卷积的，我们可以在一定的大小上训练它，并在测试期间将其应用于其他大小。批量大小设置为32。在预训练中，对于前60k个迭代，学习设置为$10^{-3}$，然后对于其余30k个迭代，学习设置为$10^{-4}$。在微调过程中，5-10k次迭代的学习速率固定为$10^{-4}$。微调迭代次数取决于数据集的大小。

由于精确召回的权衡以及数据集之间评估协议的差异，我们选择了最佳阈值α和β来优化f-measure。除了IC15之外，阈值是通过网格搜索在不同的数据集上分别选择的，其中0.1步长是在等待验证集上进行的。IC15不提供离线评估脚本，因此我们唯一的方法是向评估服务器提交多个结果。

我们的方法是用TensorFlow[1]r0.11实现的。所有的实验都在一个工作站上进行，工作站上有一个Intel Xeon 8核CPU（2.8GHz）、4个Titan X图形卡和64GB RAM。并行运行4个gpu，一批训练约0.5s，整个训练过程不到一天。

### 5.3 面向英语文本的检测

首先，我们在IC15上评估SegLink。在IC15的训练数据集上，对预训练模型进行了10k次迭代的微调。测试图像的大小调整为1280×768。我们将分segment和link的阈值分别设置为0.9和0.7。性能由官方的中央提交服务器（http://rrc.cvc.uab.es/？ch=4）。为了满足提交格式的要求，将面向输出的矩形转换为四边形。

表1列出并比较了拟议方法和其他最新方法的结果。一些结果来自在线排行榜。SegLink在很大程度上优于其它。就f-measure而言，它的表现要比第二好10.2%。考虑到有些方法比SegLink有更接近甚至更高的精度，改进主要来自于召回率。如图6所示，我们的方法能够区分文本和非常杂乱的背景。此外，SegLink由于其显式的link预测，能够正确地分离彼此非常接近的单词。

![SegLink_表1](img/SegLink_表1.png)

<center><font size=2>表1</font></center>
![SegLink_图6](img/SegLink_图6.png)

<center><font size=2>图6 IC15的示例结果。绿色区域是正确检测到的文本区域。红色的是FP或FN，灰色的是检测出来的，但是被评估算法忽略了。可视化由中央提交系统生成。黄色边框包含图像区域的缩放。</font></center>
### 5.4 多语种长行文本的检测

我们进一步证明了SegLink在非拉丁语脚本中检测长文本的能力。本实验以TD500为数据集，它由带方向的多语言文本组成。TD500的训练集只有300幅图像，这还不足以对我们的模型进行微调。我们将TD500的训练集与IC15的训练集混合，这样每一批都有一半的图像来自每个数据集。对预训练模型进行了8k次迭代的微调。测试图像大小调整为768×768。阈值α和β分别设置为0.9和0.5。绩效得分由官方开发工具包计算。

根据表2，SegLink在精度和f度量方面得分最高。得益于其完全卷积的设计，SegLink的运行速度为8.9fps，比其他速度快得多。SegLink也很简单。SegLink的推理过程是检测网络中的一个前向过程，而以往的方法[25、28、30]涉及复杂的基于规则的分组或滤波步骤。

![SegLink_表2](img/SegLink_表2.png)

<center><font size=2>表1</font></center>
TD500包含许多混合语言（英语和汉语）的长行文本。图7示出SegLink如何处理这种文本。可以看到，segment和link是沿着文本行密集检测的。它们会产生很长的边框，而这些边框很难从传统的目标探测器中获得。尽管中英文文本在外观上有很大差异，但SegLink能够同时处理它们，而无需对其结构进行任何修改。

![SegLink_图7](img/SegLink_图7.png)

<center><font size=2>图7 TD500上的示例结果。第一行显示检测到的segment和link。层内link和跨层link分别显示为红线和绿线。segment以不同颜色的矩形显示，表示不同的连接组件。第二行显示组合框。</font></center>
### 5.5 检测水平文本

最后，我们评估了SegLink在水平文本数据集上的性能。在IC13和IC15的组合训练集上，对预训练模型进行了5k迭代的微调。由于IC13中大多数文本的大小相对较大，因此测试图像的大小被调整为512×512。阈值α和β分别设置为0.6和0.3。为了匹配提交格式，我们将检测到的定向框转换为它们的轴对齐边框。

表3将SegLink与其他最新方法进行了比较。分数由中央提交系统使用“Deteval”评估协议计算。SegLink在f-measure方面取得了非常有竞争力的成绩。就f-measure而言，只有一种方法[22]优于SegLink。然而，[22]主要用于检测水平文本，不太适合带方向文本。在速度方面，SegLink在512×512图像上以超过20 FPS的速度运行，比其他方法快得多。

![SegLink_表3](img/SegLink_表3.png)

<center><font size=2>表3 IC13的结果。P、 R、F分别代表准确率、召回率和F-measure。*这些方法仅根据“ICDAR 2013”评估方案进行评估，其余方法根据“Deteval”进行评估。这两个方案通常得出非常接近的分数。</font></center>
### 5.6 局限性

SegLink的一个主要局限是需要手动设置α和β两个阈值。在实际应用中，通过网格搜索找到阈值的最优值。简化参数将是我们未来工作的一部分。另一个弱点是SegLink无法检测到字符间距非常大的文本。图8.a、b是两个这样的例子。检测到的链路连接相邻的网段，但无法连接较远的segment。图8.c示出SegLink无法检测曲线形状的文本。但是，我们认为这并不是段连接策略的局限性，而是段组合算法，目前只能产生矩形。

![SegLink_图8](img/SegLink_图8.png)

<center><font size=2>图8 TD500上的失败案例。红盒子是误报。（a）（b）SegLink无法链接字符间距较大的字符。（c）SegLink无法检测弯曲文本。</font></center>
## 6. 结论

我们提出了一种新的文本检测策略SegLink，它由一个简单高效的CNN模型实现。在水平、定向和多语种文本数据集上的优异性能很好地证明了SegLink的准确性、快速性和灵活性。在未来的研究中，我们将进一步探索其在检测弯曲文本等变形文本方面的潜力。此外，我们还对将SegLink扩展到端到端识别系统感兴趣。

## 致谢

这项工作在一定程度上得到了中国国家自然科学基金（61222308和61573160）、谷歌重点研究奖、美国焊接学会云计算研究学分、微软研究奖和Facebook设备捐赠的支持。作者还感谢中国奖学金委员会（CSC）对这项工作的支持。

## 参考文献

[1] M. Abadi, A. Agarwal, P. Barham, E. Brevdo, Z. Chen, C. Citro, G. S. Corrado, A. Davis, J. Dean, M. Devin, S. Ghemawat, I. Goodfellow, A. Harp, G. Irving, M. Isard, Y. Jia,R. Jozefowicz, L. Kaiser, M. Kudlur, J. Levenberg, D. Mane,R. Monga, S. Moore, D. Murray, C. Olah, M. Schuster,J. Shlens, B. Steiner, I. Sutskever, K. Talwar, P. Tucker,V. Vanhoucke, V. Vasudevan, F. Viegas, O. Vinyals, P. War-den, M. Wattenberg, M. Wicke, Y. Yu, and X. Zheng. TensorFlow: Large-scale machine learning on heterogeneous systems, 2015. Software available from tensorflow.org. 6
[2] A. Bissacco, M. Cummins, Y. Netzer, and H. Neven. Photoocr: Reading text in uncontrolled conditions. In ICCV,2013. 1, 2
[3] M. Busta, L. Neumann, and J. Matas. Fastext: Efficient unconstrained scene text detector. In ICCV, 2015. 8
[4] R. B. Girshick. Fast R-CNN. In ICCV, 2015. 1, 3, 5
[5] R. B. Girshick, J. Donahue, T. Darrell, and J. Malik. Rich feature hierarchies for accurate object detection and semantic segmentation. In CVPR, 2014. 1, 3
[6] A. Gupta, A. Vedaldi, and A. Zisserman. Synthetic data for text localisation in natural images. In CVPR, 2016. 1, 2, 6, 8
[7] W. Huang, Z. Lin, J. Yang, and J. Wang. Text localization in natural images using stroke feature transform and text covariance descriptors. In ICCV, 2013. 2
[8] W. Huang, Y. Qiao, and X. Tang. Robust scene text detection with convolution neural network induced MSER trees. In ECCV, 2014. 2
[9] M. Jaderberg, K. Simonyan, A. Vedaldi, and A. Zisserman. Reading text in the wild with convolutional neural networks. IJCV, 116(1):1–20, 2016. 1, 2, 8
[10] M. Jaderberg, A. Vedaldi, and A. Zisserman. Deep features for text spotting. In ECCV, 2014. 2
[11] L. Kang, Y. Li, and D. S. Doermann. Orientation robust text line detection in natural images. In CVPR, 2014. 7
[12] D. Karatzas, L. Gomez-Bigorda, A. Nicolaou, S. K. Ghosh, A. D. Bagdanov, M. Iwamura, J. Matas, L. Neumann, V. R. Chandrasekhar, S. Lu, F. Shafait, S. Uchida, and E. Valveny. ICDAR 2015 competition on robust reading. In ICDAR 2015, 2015. 2, 6
[13] D. Karatzas, F. Shafait, S. Uchida, M. Iwamura, L. G. i Bigorda, S. R. Mestre, J. Mas, D. F. Mota, J. Almazan, and ´L. de las Heras. ICDAR 2013 robust reading competition. In ICDAR 2013, 2013. 6
[14] W. Liu, D. Anguelov, D. Erhan, C. Szegedy, S. E. Reed, C. Fu, and A. C. Berg. SSD: single shot multibox detector. In ECCV, pages 21–37, 2016. 1, 3, 6
[15] J. Long, E. Shelhamer, and T. Darrell. Fully convolutional networks for semantic segmentation. In CVPR, 2015. 1
[16] L. Neumann and J. Matas. Efficient scene text localization and recognition with local character refinement. In ICDAR, 2015. 8
[17] L. Neumann and J. Matas. Real-time lexicon-free scene text localization and recognition. PAMI, 38(9):1872–1885, 2016. 2, 8
[18] J. Redmon, S. K. Divvala, R. B. Girshick, and A. Farhadi. You only look once: Unified, real-time object detection. CoRR, abs/1506.02640, 2015. 3, 6
[19] S. Ren, K. He, R. B. Girshick, and J. Sun. Faster R-CNN: towards real-time object detection with region proposal networks. In NIPS, 2015. 1, 3
[20] A. Shrivastava, A. Gupta, and R. B. Girshick. Training region-based object detectors with online hard example mining. In CVPR, 2016. 6
[21] K. Simonyan and A. Zisserman. Very deep convolutional networks for large-scale image recognition. CoRR, abs/1409.1556, 2014. 2, 3
[22] Z. Tian, W. Huang, T. He, P. He, and Y. Qiao. Detecting text in natural image with connectionist text proposal network. In ECCV, 2016. 1, 2, 3, 7, 8
[23] K. Wang and S. J. Belongie. Word spotting in the wild. In ECCV, 2010. 2
[24] T. Wang, D. J. Wu, A. Coates, and A. Y. Ng. End-to-end text recognition with convolutional neural networks. In ICPR, 2012. 2
[25] C. Yao, X. Bai, W. Liu, Y. Ma, and Z. Tu. Detecting texts of arbitrary orientations in natural images. In CVPR, 2012. 1, 2, 6, 7
[26] C. Yao, X. Bai, N. Sang, X. Zhou, S. Zhou, and Z. Cao. Scene text detection via holistic, multi-channel prediction. CoRR, abs/1606.09002, 2016. 2, 3, 7
[27] X. Yin, W. Pei, J. Zhang, and H. Hao. Multi-orientation scene text detection with adaptive clustering. PAMI, 37(9):1930–1937, 2015. 7
[28] X. Yin, X. Yin, K. Huang, and H. Hao. Robust text detection in natural scene images. PAMI, 36(5):970–983, 2014. 7
[29] Z. Zhang, W. Shen, C. Yao, and X. Bai. Symmetry-based text line detection in natural scenes. In CVPR, 2015. 2, 3, 8
[30] Z. Zhang, C. Zhang, W. Shen, C. Yao, W. Liu, and X. Bai. Multi-oriented text detection with fully convolutional networks. In CVPR, 2016. 1, 2, 3, 7, 8