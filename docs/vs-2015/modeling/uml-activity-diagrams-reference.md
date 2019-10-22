---
title: UML 活动图：引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.activitydiagram.diagram
- vs.teamarch.activitydiagram.toolbox
- vs.teamarch.UMLModelExplorer.activitydiagram
helpviewer_keywords:
- UML diagrams, activity
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- activity diagrams
- UML, activity diagrams
- behaviors, UML
ms.assetid: 07efcd17-2a96-4052-9957-6dcccbb725ee
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3a882867720e9cca2d51419643ebe60e692817a1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658454"
---
# <a name="uml-activity-diagrams-reference"></a>UML 活动图：参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*活动图*通过一系列操作将业务流程或软件进程显示为工作流。 用户、软件组件或计算机可以执行这些操作。

 使用活动图可以像下面示例一样描述多种类型的进程：

- 用户和你的系统间的业务流程或工作流。 有关详细信息，请参阅[模型用户需求](../modeling/model-user-requirements.md)。

- 用例中所执行的步骤。 有关详细信息，请参阅[UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)。

- 软件协议，即得到允许的组件间的交互序列。

- 软件算法。

  本主题介绍了可以在活动图中使用的元素。 有关绘制活动图的详细信息，请参阅[UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)。 若要创建 UML 活动图，请在 "**体系结构**" 菜单上单击 "**新建 UML 或层关系图**"。 有关如何一般绘制建模图的详细信息，请参阅[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)。

## <a name="reading-activity-diagrams"></a>读取活动图
 以下各节中的表介绍了可以在活动图上使用的元素以及它们的主要属性。 有关元素属性的完整列表，请参阅[UML 活动图上元素的属性](../modeling/properties-of-elements-on-uml-activity-diagrams.md)。

 活动图中显示的操作和其他元素构成一个活动。 可以在 UML 模型资源管理器中查看活动。 它是在你将第一个元素添加到关系图时创建的。

 读取关系图时，假设有一个令牌或控制线程将连接线从一个操作传递给下一个操作。

### <a name="simple-control-flows"></a>简单的控制流
 可以用分支和循环显示一系列操作。 有关如何使用此处所述的元素的详细信息，请参阅主题中的 " [UML 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)" 的 "描述控制流" 一节。

 ![简单的控制流](../modeling/media/uml-actovsimple.png "UML_ActOvSimple")

||||
|-|-|-|
|**整形**|**元素**|**Description 和 Main 属性**|
|1|**操作**|活动中的一个步骤，用户或软件可以在其中执行某些任务。<br /><br /> 操作可以在令牌到达其所有传入流时开始。 操作结束后，令牌会在所有传出流上进行发送。<br /><br /> -   **正文**-指定详细操作。<br />-   **language** -正文中的表达式的语言。<br />-   **本地后置**条件-执行结束时必须满足的约束。 操作实现的目标。<br />-   **本地前提条件**-执行开始之前必须满足的约束。|
|2|**控制流**|显示操作之间的控制流的连接线。 为了解释关系图，假设有一个令牌从一个操作流向下一个操作。<br /><br /> 若要创建控制流，请使用**连接器**工具。|
|3|**初始节点**|指示活动中的第一个操作或第一批操作。 活动开始时，令牌从初始节点流出。|
|4|**活动最终节点**|活动结束。 令牌到达时，活动将终止。|
|5|**决策节点**|流中的一个条件分支。 具有一个输入以及两个或多个输出。 传入令牌只会在一个输出上显示。|
|6|**预防**|一个用于指定令牌是否可以沿连接线流动的条件。 在决策节点的传出流上最常用到。<br /><br /> 若要设置临界，请右键单击流，单击 "**属性**"，然后设置 "**临界**" 属性。|
|7|**合并节点**|在合并由决策节点拆分的流时需要用到。 具有两个或多个输入以及一个输出。 任何输入上的令牌都会在输出上显示。|
|8|**注释**|提供有关其链接到的元素的其他信息。|
|9|**调用行为操作**|一种在另一个活动图中进行了更加详细定义的操作。<br /><br /> -   **IsSynchronous** -如果为 true，则操作将等待，直到活动终止。<br />-   **行为**-调用的活动。|
|（不显示）|**调用操作操作**|一种可以在类的实例上调用操作的操作。|
||**活动**|活动图所描绘的工作流。 若要查看活动的属性，必须在 " **UML 模型资源管理器**" 中选择该活动。<br /><br /> -   **是只读**的-如果为 true，则活动不应更改任何对象的状态。<br />-   **是单次执行**的-如果为 true，则一次最多会执行一次此关系图。|
||**UML 活动图**|显示活动的关系图。 若要查看其属性，请单击该关系图的空白部分。 **注意：** 活动图的名称、包含关系图的文件和关系图显示的活动都可以是不同的。|

### <a name="concurrent-flows"></a>并发流
 可以描述同时执行的一系列操作。 有关相关信息，请参阅“绘制并发流”。

 ![显示并发流的活动图](../modeling/media/uml-actovconcurrent.png "UML_ActovConcurrent")

||||
|-|-|-|
|**整形**|**元素**|**描述**|
|11|**分叉节点**|将单个流划分为并发流。 每个传入令牌会在每个传出连接线上生成一个令牌。|
|12|**联接节点**|将并发流合并为单个流。 当每个传入流有等待的令牌时，输出上就会生成一个令牌。|
|13|**发送信号操作**|一种可以将消息或信号发送给另一个活动，或同一活动中的并发线程的操作。 操作的标题或其他注释中指定的信息包含了消息的类型和内容。<br /><br /> 此操作能够以信号形式发送数据，信号可以传递给对象流或输入插针 (16) 中的操作。|
|14|**接受事件操作**|一种要在等到消息或信号后才能继续执行的操作。 标题或其他注释中指定的信息包含了此操作能接收的消息类型。<br /><br /> 如果此操作没有传入控制流，它会在收到消息后立即生成一个令牌。<br /><br /> 此操作能够以信号形式接收数据，信号可以在对象流或输出插针 (17) 中进行传递。<br /><br /> -   **IsUnmarshall** -如果为 true，则可以有多个类型化的输出插针，并且数据打乱到它们上。 如果为 False，则所有数据都显示在一个插针上。|

### <a name="DataFlow"></a>数据流
 可以描述从一个操作到另一个操作的数据流。 有关此节中所用元素的更多信息，请参见“绘制活动图指南”主题的“绘制数据流”一节。

 ![显示数据流的活动图](../modeling/media/uml-actovdata.png "UML_ActOvData")

||||
|-|-|-|
|**整形**|**元素**|**描述**|
|15|**对象节点**|表示通过流传递的数据。<br /><br /> -   **排序**-如何存储多个令牌。<br />-   **选择**-调用可在另一个关系图中定义的进程，该进程可对数据进行筛选。<br />-   **上限**-0 指示数据必须沿流直接传递; \* 指示可将数据存储在流中。<br />-   **类型**-存储和传输的对象的类型。|
|16|**输入插针**|表示操作执行时可以接收的数据。<br /><br /> -   **类型**-传输的对象的类型。|
|17|**输出插针**|表示操作执行时生成的数据。<br /><br /> -   **类型**-传输的对象的类型。|
|18|**活动参数节点**|一种对象节点，通过该节点活动可以接收或生成数据。<br /><br /> 在通过另一个活动调用此关系图表示的活动时使用，或在此关系图描述操作或函数时使用。<br /><br /> -   **类型**-传输的对象的类型。|
|（不显示）|**对象流**|显示操作和对象节点之间的数据流的连接线。<br /><br /> 若要创建对象流，请使用**连接器**工具将输入或输出插针或对象节点链接到另一个元素。<br /><br /> -   **选择**-调用可在另一个关系图中定义的进程，该进程可对数据进行筛选。<br />-   **转换**-调用可在另一个关系图中定义的进程，该进程可对数据进行转换。<br />-   **IsMulticast** -表示可能有多个收件人对象或组件。<br />-   **IsMultiReceive** -表示可能从多个对象或组件接收输入。|

## <a name="see-also"></a>请参阅
 [编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md) [uml 活动图：准则](../modeling/uml-activity-diagrams-guidelines.md)
