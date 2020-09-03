---
title: UML 活动图上元素的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.activitydiagram.shapes.properties
helpviewer_keywords:
- UML, element properties
- activity diagrams, properties
ms.assetid: 9849d45e-65d5-46bd-a319-757e90b7c748
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6698f728645d5fb9a38d2a003293c7fadda005d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671444"
---
# <a name="properties-of-elements-on-uml-activity-diagrams"></a>UML 活动图上元素的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 活动图上的每个元素都有属性。 若要查看某个元素的属性，请在关系图或 " **UML 模型资源管理器** " 中右键单击该元素，然后单击 " **属性**"。 属性将显示在 " **属性** " 窗口中。

> [!NOTE]
> 本主题主要讲述 UML 活动图上元素的属性。 有关如何读取 UML 活动图的信息，请参阅 [Uml 活动图：参考](../modeling/uml-activity-diagrams-reference.md)。 有关如何绘制 UML 活动图的详细信息，请参阅 [Uml 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)。

## <a name="properties-of-elements"></a>元素的属性

|         属性         |        默认         |                               元素                               |                                                                                                                                                                说明                                                                                                                                                                 |
|--------------------------|------------------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         **名称**         |     默认名称     |                                 All                                 |                                                                                                                                                          标识元素。                                                                                                                                                           |
|    **限定的名称**    |    Package :: Name     |                                 All                                 |                                                                                                                     唯一标识元素。 以包含它的包的限定名为前缀。                                                                                                                     |
|      **工作项**      |      0 associated      |                                 All                                 |                                                                                与此元素关联的工作项的数目。 若要关联工作项，请参阅 [链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。                                                                                |
|     **说明**      |         （无）         |                                 All                                 |                                                                                                                                             可在此处记下有关元素的常规说明。                                                                                                                                             |
|        **颜色**         | （该类型的默认值） |                                 All                                 |                                                                                                                                                          形状的颜色。                                                                                                                                                           |
|         **正文**         |         （无）         |                               操作                                |                                                                                                                                                      指定详细操作。                                                                                                                                                       |
|       **语言**       |         （无）         |                               操作                                |                                                                                                                                                  正文中的表达式的语言。                                                                                                                                                   |
| **本地后置条件** |         （无）         |         操作，发送，接受，调用行为，调用操作         |                                                                                                                          执行结束时必须满足的约束。 操作实现的目标。                                                                                                                          |
| **本地前置条件**  |         （无）         |         操作，发送，接受，调用行为，调用操作         |                                                                                                                                        执行开始之前必须满足的约束。                                                                                                                                         |
|    **是否同步**    |          正确          |                    调用行为，调用操作                    |                                                                                                                                        -如果为 true，则操作将等待，直到活动终止。                                                                                                                                        |
|       **行为**       |         （无）         |                            调用行为                            |                                                                                                                                                         -调用的活动。                                                                                                                                                          |
|      **操作**       |         （无）         |                           调用操作                            |                                                                                                                                                         -调用的操作。                                                                                                                                                         |
|    **Is Unmarshall**     |         错误          |                            接受事件                             |                                                                                                       -如果为 true，则可以有多个类型化的输出插针，数据将取消封送到它们。 如果为 False，则所有数据都显示在一个插针上。                                                                                                        |
|     **上限**      |        **\\**\*        |                   对象节点，活动参数                   |                                                                                                      **0** 指示数据必须直接沿流传递。<br /><br /> **\\**\* 指示可以将数据存储在流中。                                                                                                      |
|      **选择**       |         （无）         | 对象节点，活动参数，输入插针，输出插针，对象流 |                                                                                                                          调用筛选数据的进程。 此进程可以在另一个关系图中定义。                                                                                                                          |
|       **中间件排序**       |         （无）         |       对象节点，活动参数，输入插针，输出插针        |                                                                                                                                                    -如何存储多个令牌。                                                                                                                                                     |
|      **Is Control**      |         错误          |                        输入插针，输出插针                        |                                                                                                                            -如果为 true，则此插针上的流为控制流。 如果为 False，则为对象流。                                                                                                                            |
|         **类型**         |         （无）         |       输入插针，输出插针，对象节点，活动参数        |                              -传输的对象的类型。<br />-类型可以是基元类型（如整数），也可以是在模型中的其他位置定义的分类器。 如果输入未定义的类型的名称，该名称将显示在 UML 模型资源管理器的 " **未指定的类型** " 部分中。                               |
|     **多重性**     |           1            |                        输入插针，输出插针                        | -可以是单个值或范围 `[n..m]` 。<br />-下限 `n` -此操作无法启动输入插针 () 或停止输出) 插针 (，直到有 `n` 对象在等待。<br />-上限 `m` -操作 `m` 在一个执行中无法使用或生成多个对象。 \* 表示没有限制。 |
|    **转换**    |         （无）         |                             对象流                             |                                                                                                                      -调用转换数据的进程。 此进程可以在另一个关系图中定义。                                                                                                                       |
|     **Is Multicast**     |         错误          |                             对象流                             |                                                                                                                                 -指示可能有多个收件人对象或组件。                                                                                                                                 |
|   **Is MultiReceive**    |         错误          |                             对象流                             |                                                                                                                                 -指示可能有多个收件人对象或组件。                                                                                                                                 |
| **Is Single Execution**  |         错误          |                          活动图                           |                                                                                                                                   -如果设置，一次此关系图最多可执行一次。                                                                                                                                    |

## <a name="see-also"></a>另请参阅
 [Uml 活动图：引用](../modeling/uml-activity-diagrams-reference.md) [uml 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)
