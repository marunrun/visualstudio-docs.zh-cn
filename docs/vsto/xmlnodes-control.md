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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840805"
---
# <a name="xmlnodes-control"></a>XMLNodes 控件
  **重要提示** 本主题中的关于 Microsoft Word 的信息是专门为其提供的个人和美国组织的权益和使用的，也就是在 Microsoft word 产品（在2010年1月之前）中运行的、microsoft Word 产品，microsoft Word 产品在年1月之前获得的 microsoft Word 产品，microsoft word 产品在 microsoft word 中删除了与自定义 与 Microsoft Word 有关的信息可能不会被美国或其所在区域中的个人或组织阅读或使用，或开发在 Microsoft Word 产品上运行的、2010年1月10日之后的 microsoft Word 产品。对于该日期之前许可的产品，这些产品的行为并不相同，也不会在美国之外购买和许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNodes>控件是公开事件的映射 XML 节点对象的集合。 <xref:Microsoft.Office.Tools.Word.XMLNodes>仅在将重复架构元素映射到 Microsoft Office Word 文档时，才创建控件。 如果重复元素包含子元素，则还会以控件的形式创建每个子元素 <xref:Microsoft.Office.Tools.Word.XMLNodes> 。

 在 Visual Studio 创建 XML 节点的集合后，可以直接对控件编程而无需遍历 Word 对象模型。 <xref:Microsoft.Office.Tools.Word.XMLNodes>只能通过从文档中删除元素映射来删除控件。

> [!NOTE]
> 如果通过属性访问控件的子元素 <xref:Microsoft.Office.Tools.Word.XMLNodes> <xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A> ，则它将返回 <xref:Microsoft.Office.Interop.Word.XMLNode> 对象，而不是 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 有关详细信息，请参阅 [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Word.XMLNodes>控件不支持数据绑定。 这是因为该 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件没有复杂的数据绑定功能，并且简单的数据绑定不能表示重复数据。

## <a name="formatting"></a>格式化
 可应用于文档中的文本的任何格式设置都可以应用于 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件。

## <a name="events"></a>事件
 可用于该控件的事件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 包括：

- <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>

## <a name="compare-events"></a>比较事件
 当用户将其光标移到特定控件的上下文中时，可以捕获事件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 。 例如，你可能有一个 <xref:Microsoft.Office.Tools.Word.XMLNodes> 名为 `Customer` 的控件，该控件有一个 <xref:Microsoft.Office.Tools.Word.XMLNodes> 名为的子控件 `Company` ，并 `Company` 有两个 <xref:Microsoft.Office.Tools.Word.XMLNodes> 名为的子控件， `CompanyName` `CompanyRegion` 如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果您想要在每次将光标移到节点时在 "操作" 窗格上显示一个控件，是将 `Company` 游标置于 `CompanyName` 还是的上下文中是不重要的 `CompanyRegion` `Company` 。 在这种情况下，你可以在的事件中编写代码 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> `Company` 。

 在大多数情况下，当光标进入 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件时，将 <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> 引发和 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> 事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|当光标放置在 <xref:Microsoft.Office.Tools.Word.XMLNodes> 集合的一个节点中时发生此事件。|当光标从节点上下文以外的区域移入 <xref:Microsoft.Office.Tools.Word.XMLNodes> 集合的节点或子代节点之一时发生。 换而言之，仅当上下文发生更改时才引发，多个嵌套控件可以引发 <xref:Microsoft.Office.Tools.Word.XMLNodes> 。|

 例如，当你将光标从外移到时 `Customer` `CompanyName` ，将 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> `Customer` 引发、和的事件 `Company` `CompanyName` 。 如果随后将游标从移 `CompanyName` 到 `CompanyRegion` ，则 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> 只引发的事件 `CompanyRegion` ，因为上下文对于和都是相同的 `Company` `Customer` 。 文档中可以有多个 `Company` 节点。 如果将游标从 `CompanyName` 一个节点移 `Company` 到另一个节点的节点 `CompanyName` ，则 `Company` 上下文是相同的，因此只 <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> 会引发事件。

 事件与事件之间的差异相同 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave> <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect> 。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNode 控件](../vsto/xmlnode-control.md)
- [如何：将 XMLNodes 控件添加到 Word 文档](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [如何：将架构映射到 Visual Studio 中的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
