---
title: XMLNodes 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, events
- XMLNodes control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9ad16165924a33a25dab2b1cfb49a0a7bbfe0875
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421539"
---
# <a name="xmlnodes-control"></a>XMLNodes 控件
  **重要**设置 Microsoft Word 有关本主题中的信息是提供的以独占方式适合的权益和使用个人和组织用户位于美国州和其领土的外部或使用，或开发运行的程序，在 2010 年 1 月，Microsoft 中删除的特定功能实现的时间之前已由 Microsoft 许可的 Microsoft Word 产品被与 Microsoft Word 中的自定义 XML。 有关 Microsoft Word 此信息可能不读取或使用的个人或组织在美国或其区域使用，或开发在 Microsoft Word 2010 年 1 月 10 日之后，由 Microsoft 已许可的产品运行的程序中;这些产品不将行为与相同产品许可在该日期之前或购买，美国以外的使用许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNodes>控件是公开事件映射 XML 节点对象的集合。 <xref:Microsoft.Office.Tools.Word.XMLNodes>仅时重复架构元素映射到 Microsoft Office Word 文档中创建控件。 如果重复元素包含子元素，每个的子元素将创建为<xref:Microsoft.Office.Tools.Word.XMLNodes>控件。

 Visual Studio 创建的 XML 节点集合后，可以对其进行编程控制直接而无需遍历 Word 对象模型。 <xref:Microsoft.Office.Tools.Word.XMLNodes>可以仅通过从文档中移除的元素映射删除控件。

> [!NOTE]
> 如果您访问的子元素<xref:Microsoft.Office.Tools.Word.XMLNodes>通过控制<xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A>属性，它将返回<xref:Microsoft.Office.Interop.Word.XMLNode>对象而非<xref:Microsoft.Office.Tools.Word.XMLNode>控件。 有关详细信息，请参阅[主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Word.XMLNodes>控件不支持数据绑定。 这是因为<xref:Microsoft.Office.Tools.Word.XMLNodes>控件不具有复杂数据绑定功能，并简单数据绑定不能表示重复数据。

## <a name="formatting"></a>格式化
 可以对文档中的文本应用任何格式设置可应用于<xref:Microsoft.Office.Tools.Word.XMLNodes>控件。

## <a name="events"></a>事件
 可用于事件<xref:Microsoft.Office.Tools.Word.XMLNodes>控制是：

- <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>

## <a name="compare-events"></a>比较事件
 您可以捕获事件时用户将他或她的特定上下文中的光标移动<xref:Microsoft.Office.Tools.Word.XMLNodes>控件。 例如，可能有<xref:Microsoft.Office.Tools.Word.XMLNodes>控件命名为`Customer`具有子级<xref:Microsoft.Office.Tools.Word.XMLNodes>名为控件`Company`，并`Company`具有两个子<xref:Microsoft.Office.Tools.Word.XMLNodes>控件分别命名为`CompanyName`和`CompanyRegion`，如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果你想要显示操作窗格上的控件只要将光标移到`Company`节点，并应重要是否将光标置于`CompanyName`或`CompanyRegion`因为它们的上下文中都是`Company`。 在这种情况下，可以编写代码<xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>事件的`Company`。

 在大多数情况下，当光标进入<xref:Microsoft.Office.Tools.Word.XMLNodes>控件，同时<xref:Microsoft.Office.Tools.Word.XMLNodes.Select>和<xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>引发事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|当光标放置在的节点之一时发生<xref:Microsoft.Office.Tools.Word.XMLNodes>集合。|当光标放置在节点或子代节点之一时发生<xref:Microsoft.Office.Tools.Word.XMLNodes>集合，从节点的上下文以外的区域。 换而言之，它只更改时引发的上下文，并可以对多个嵌套引发<xref:Microsoft.Office.Tools.Word.XMLNodes>控件。|

 例如，当移动光标从外部`Customer`成`CompanyName`，则<xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>事件`Customer`， `Company`，和`CompanyName`引发。 如果将光标从然后移动`CompanyName`到`CompanyRegion`，则<xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>仅对事件`CompanyRegion`引发，因为上下文为两个相同`Company`和`Customer`。 可以有多个`Company`在文档中的节点。 如果您将从光标移`CompanyName`之一的节点`Company`到`CompanyName`的另一个节点`Company`，上下文是相同的因此，只有<xref:Microsoft.Office.Tools.Word.XMLNodes.Select>引发事件。

 之间存在相同的差异<xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>事件和<xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>事件。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNode 控件](../vsto/xmlnode-control.md)
- [如何：向 Word 文档添加 XMLNodes 控件](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [如何：将架构映射到 Visual Studio 内部的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
