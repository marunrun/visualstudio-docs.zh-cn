---
title: 代码度量值类耦合
ms.date: 1/8/2021
description: 了解 Visual Studio 中代码度量值的类耦合指标。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db1308843cb3c4fe8fb0a4aa32300e545e5e3a7c
ms.sourcegitcommit: b1f7e7d7a0550d5c6f46adff3bddd44bc1d6ee1c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "98069518"
---
# <a name="code-metrics---class-coupling"></a>代码度量值类耦合

类耦合还按最初由 [CK94](#ck94)定义的对象之间的名称耦合 (CBO) 。 实质上，类耦合是单个类使用的类的度量值。 较高的数字是错误的，并且此指标通常很少。 类耦合已经显示为软件故障的准确预测，最新研究表明，上限值9是最有效的 [S2010](#s2010)。

根据 Microsoft 文档，类耦合 "通过参数、本地变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、在外部类型上定义的字段和特性修饰来度量与唯一类的耦合。 优秀的软件设计要求类型和方法应具有较高的聚合和低耦合。 高耦合性表明，由于它对其他类型的互依关系，难于重复使用和维护的设计。 "

耦合和聚合的概念是明显相关的。 若要讨论本主题，我们将不会深入了解聚合，而不是从 [KKLS2000](#kkls2000)提供简要定义：

"Module 聚合由 Yourdon 和 Constantine 引入了一个模块的内部元素与另一个" [YC79](#yc79)的紧密绑定或关联。 如果某个模块只表示一个任务 [...]，并且它的所有元素都参与此项任务，则该模块具有强聚合。 它们将聚合描述为设计的属性，而不是代码，以及可用于预测可重用性、可维护性和可更改性的属性。

## <a name="class-coupling-example"></a>类耦合示例

让我们看看操作中的类耦合。 首先，创建一个新的控制台应用程序，创建一个名为 Person 的新类，其中包含一些属性，然后立即计算代码度量值：

![类耦合示例1](media/class-coupling-example-1.png)

请注意，类耦合为0，因为该类不使用任何其他类。 现在，创建另一个名为 PersonStuff 的类，该方法具有创建 Person 实例并设置属性值的方法。 再次计算代码度量值：

![类耦合示例2](media/class-coupling-example-2.png)

了解类耦合值如何呢？ 另请注意，无论你设置的属性有多少，类耦合值只会向上提升1而不是其他值。 类耦合仅针对此指标测量一次每个类，而不管使用的数量是多少。 此外，你是否可以看到 `DoSomething()` 有1个，但构造函数的 `PersonStuff()` 值为0？ 当前构造函数中没有使用其他类的代码。

如果使用其他类将代码放入构造函数中，该怎么办？ 下面是你获取的内容：

![类耦合示例3](media/class-coupling-example-3.png)

现在构造函数清楚地包含了使用其他类的代码，类耦合指标显示了这一事实。 同样，你可以查看的整体类耦合为 `PersonStuff()` 1， `DoSomething()` 也可以显示为1，表明无论你使用它的内部代码有多少，都只有一个外部类在使用中。

接下来，创建另一个新类。 为此类指定一个名称，并在其中创建一些属性：

![类耦合示例-添加新类](media/class-coupling-example-add-new-class.png)

现在，在 `DoSomething()` 类的方法中使用类 `PersonStuff` ，并再次计算代码度量值：

![类耦合示例4](media/class-coupling-example-4.png)

如您所见，PersonStuff 类的类耦合最多可达2个，并且，如果您钻取到类中，就会看到该 `DoSomething()` 方法的耦合最多，但构造函数仍只使用1个类。  使用这些度量值，可以查看给定类的总最大数量，并向下钻取每个成员的详细信息。

## <a name="the-magic-number"></a>幻数

与圈复杂度一样，没有适合所有组织的限制。 但是， [S2010](#s2010) 确实表明限制为9：

"因此，我们认为阈值为 [...]最有效的。  (单个成员) 的这些阈值为 CBO = 9 [...]。 添加的 (强调) 

## <a name="code-analysis"></a>代码分析

代码分析包括一类可维护性规则。 有关详细信息，请参阅可 [维护性规则](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)。 使用旧代码分析时，扩展的设计准则规则集包含可维护性区域：

![类耦合扩展的设计准则规则](media/class-coupling-extended-design-guideline-rules.png)

可维护性区域内是类耦合的规则：

![类耦合规则](media/class-coupling-maintainability-area-rules.png)

当类耦合过多时，此规则会发出警告。 有关详细信息，请参阅 [CA1506：避免过度类耦合](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)。

有关此规则的说明，请参阅已存档的代码分析博客文章：将 [代码度量值作为签入策略](/archive/blogs/codeanalysis/code-metrics-as-check-in-policy) ，并在 *类和更高的 80* 上为方法提供阈值说明警告。  这些值看似异常高，但至少提供极高的上限。 如果出现此警告，则几乎肯定会出现问题。

## <a name="citations"></a>引文

### <a name="ck94"></a>CK94

Chidamber，S. R。 & Kemerer，c。  (1994) 。 用于面向对象的设计的指标套件 (软件工程上的 IEEE 事务， 6) 。 从 Pittsburgh 网站的大学检索到5月14日2011： [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili、H.、Keller、R.、Lustman、、Denis (2000) 。 类聚合再次检查：有关工业系统的实践调查，请 (《 Object-Oriented 软件工程) 的定量方法的调查。 从 Université de Montréal 网站检索到年5月20日2011 [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam、& Krishnan、M. S。 (2003). Object-Oriented 设计复杂性的 CK 指标的经验分析：软件设计 (IEEE 事务上的软件缺陷的影响， 4) 。 从马萨诸塞州 Dartmouth 网站的大学那里检索5月14日2011 [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi、 (2010) 。 调查 Open-Source 系统中的 Object-Oriented 指标的可接受风险级别， (软件工程，36，无。 2) 。

### <a name="yc79"></a>YC79

Edward Yourdon 和 Larry Constantine。 结构化设计。 Prentice 厅、Englewood Cliffs、N.J.、1979。