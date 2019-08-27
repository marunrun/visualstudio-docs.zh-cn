---
title: 使用 DSL 定义关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.diagram
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language Tools, diagram
- Domain-Specific Language Tools, Split Tree
- Domain-Specific Language Tools, Show Map Lines
- Domain-Specific Language Tools, Show As Class
- Domain-Specific Language Tools, Bring Tree Here
ms.assetid: 1a4c7a58-e134-438e-848e-efd98f92bf10
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd4b15fb7c0f1cbc0630779ecef0373977bb2056
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694210"
---
# <a name="working-with-the-dsl-definition-diagram"></a>使用 DSL 定义图表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

关系图的[!INCLUDE[dsl](../includes/dsl-md.md)]定义是用于定义特定于域的语言的重要工具。 你可以将元素添加到域模型并定义关系图上的关系，也可以修改关系图的布局以使其更具可读性。  
  
## <a name="the-layout-of-the-diagram"></a>关系图的布局  
 [!INCLUDE[dsl](../includes/dsl-md.md)]定义关系图有两个分区**类和关系**分区并**关系图元素**分区。 **类和关系**分区显示域类、 域关系和继承。 **关系图元素**分区显示形状类、 连接符类、 泳道类和生成的设计器关系图。  
  
 域类可以出现在多个位置中**类和关系**分区。 如果域类是其他域类的基类，则域类定义将显示继承树；如果域类是嵌入或引用关系的源，则其定义将显示关系树。 域类占位符将显示为嵌入或引用关系的目标。 默认情况下，占位符元素显示与**域属性**折叠隔离舱。 它们不显示继承，也不显示嵌入或引用关系。  
  
 当添加域类时，它将显示在下半部分**类和关系**分区。 当添加一个嵌入或引用关系时，它将绘制在源域类的下方和右侧。  
  
 当添加域类和关系时，可能很难找到某个特定的域类。 您可以通过右键单击该中查找域类**DSL 资源管理器**，然后单击**关系图中的定位**。  
  
 以下部分介绍了如何更改关系图的外观以使其更易于阅读。  
  
## <a name="copying-elements"></a>复制元素  
 可以对 DSL 定义关系图中的元素使用复制、剪切和粘贴。  
  
## <a name="zooming-in-or-out-on-the-diagram"></a>在关系图上放大或缩小  
 可以由使用放大或缩小关系图**DSL 设计器**工具栏来设置缩放级别。  
  
## <a name="hiding-map-lines"></a>隐藏地图线条  
 地图线条是在域类或域关系与其映射到的形状或连接符之间绘制的线条。 您可以通过单击隐藏地图线条**显示地图线条**按钮**DSL 设计器**工具栏。 若要显示这些线条，请再次单击该按钮。  
  
## <a name="changing-the-diagram-layout"></a>更改关系图布局  
 可以更改的版式**类和关系**分区，如下所示。  
  
### <a name="expandcollapse"></a>展开/折叠  
 可以减少通过右键单击它，然后单击表示域类或形状的隔离舱形状元素的大小**折叠**。 这将隐藏**域属性**形状的隔离舱。 若要显示**域属性**再次隔离舱，右键单击该形状，然后单击**展开**。  
  
### <a name="move-updown"></a>上移/下移  
 可以通过右键单击该元素，然后单击在分区中来移动域类或关系图元素向上或向下**移**或**下移**。 如果你要移动显示为嵌入或引用关系的目标的占位符元素，则关系将随它一起移动。  
  
### <a name="expandcollapse-relationships-tree"></a>展开/折叠关系树  
 如果域类与其他域类的嵌入或引用关系中扮演源角色，则可以通过右键单击该域类定义，然后单击隐藏关系**折叠关系树**。 要显示的关系，右键单击定义元素，然后单击**展开关系树**。  
  
### <a name="expandcollapse-inheritance-tree"></a>展开/折叠继承树  
 如果域类是其他域类的基类，则可以通过右键单击该域类定义，然后单击隐藏继承树**折叠继承树**。 若要显示继承树，右键单击定义元素，然后单击**展开继承树**。  
  
### <a name="bring-tree-here"></a>将树放在此处  
 可以通过右键单击占位符域类，然后单击合并关系图**将树放在此处**。 该占位符域类将成为定义元素并显示继承和关系树。 如果前一个定义元素是关系的目标元素或继承关系中的子元素，则它将成为占位符元素；否则，它将消失。  
  
### <a name="split-tree"></a>Split Tree  
 您可通过右键单击显示它们的域类定义，然后单击中断继承或关系树**拆分树**。 该定义元素将成为占位符元素，并且定义域类连同其继承和关系树现在都可显示在分区底部。  
  
### <a name="show-as-class"></a>显示为类  
 如果域关系有派生关系，或如果它具有与其他域关系的嵌入或引用关系，您可以显示此关系为一个类，通过右键单击该关系，然后单击**显示为类**. 将会显示此关系**域属性**隔离舱，将显示继承和关系树。  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
