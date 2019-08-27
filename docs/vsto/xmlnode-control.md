---
title: XMLNode 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a8bd5c4612b59f909ae623eb4092a209798f98c5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975726"
---
# <a name="xmlnode-control"></a>XMLNode 控件
  **重要**设置 Microsoft Word 有关本主题中的信息是提供的以独占方式适合的权益和使用个人和组织用户位于美国州和其领土的外部或使用，或开发运行的程序，在 2010 年 1 月，Microsoft 中删除的特定功能实现的时间之前已由 Microsoft 许可的 Microsoft Word 产品被与 Microsoft Word 中的自定义 XML。 有关 Microsoft Word 此信息可能不读取或使用的个人或组织在美国或其区域使用，或开发在 Microsoft Word 2010 年 1 月 10 日之后，由 Microsoft 已许可的产品运行的程序中;这些产品不将行为与相同产品许可在该日期之前或购买，美国以外的使用许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNode>控件是公开事件并可以绑定到数据的映射的 XML 节点对象。 <xref:Microsoft.Office.Tools.Word.XMLNode>仅当非重复架构元素映射到 Microsoft Office Word 文档时创建控件。 Visual Studio 创建的 XML 节点后，你可以针对它编程直接而无需遍历 Word 对象模型。

 <xref:Microsoft.Office.Tools.Word.XMLNode>可以仅通过在 Word 中删除的元素映射删除控件。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Word.XMLNode>控件支持简单数据绑定。 XML 节点应使用绑定到数据源<xref:System.Windows.Forms.IBindableComponent.DataBindings%2A>属性。 如果更新绑定数据集内的数据，则 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件会反映所做的更改。

## <a name="formatting"></a>格式化
 格式设置可以应用于<xref:Microsoft.Office.Interop.Word.XMLNode>对象可应用于<xref:Microsoft.Office.Tools.Word.XMLNode>控件。 这包括字体、 下划线样式和字符样式。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件：

- <xref:Microsoft.Office.Tools.Word.XMLNode.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ValidationError>

## <a name="compare-events"></a>比较事件
 您可以捕获事件时用户将他或她的特定上下文中的光标移动<xref:Microsoft.Office.Tools.Word.XMLNode>控件。 例如，可能有<xref:Microsoft.Office.Tools.Word.XMLNode>控件命名为`Customer`具有子级<xref:Microsoft.Office.Tools.Word.XMLNode>名为控件`Company`，并`Company`具有两个子<xref:Microsoft.Office.Tools.Word.XMLNode>控件分别命名为`CompanyName`和`CompanyRegion`，如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果你想要显示操作窗格上的控件只要将光标移到`Company`节点，并应重要是否将光标置于`CompanyName`或`CompanyRegion`因为它们的上下文中都是`Company`。 在这种情况下，可以编写代码<xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>事件的`Company`。

 在大多数情况下，当光标进入<xref:Microsoft.Office.Tools.Word.XMLNode>控件，同时<xref:Microsoft.Office.Tools.Word.XMLNode.Select>和<xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>引发事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|将光标置于时发生<xref:Microsoft.Office.Tools.Word.XMLNode>。|将光标置于时发生<xref:Microsoft.Office.Tools.Word.XMLNode>或其中一个子代节点，从节点的上下文以外的区域。 换而言之，它只更改时引发的上下文。|

 例如，当移动光标从外部`Customer`成`CompanyName`，则<xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>事件`Customer`， `Company`，和`CompanyName`引发。 如果将光标从然后移动`CompanyName`到`CompanyRegion`，则只<xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>事件`CompanyRegion`因为这两者的上下文中仍会引发`Company`和`Customer`。

 之间存在相同的差异<xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>事件和<xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>事件。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNodes 控件](../vsto/xmlnodes-control.md)
- [如何：向 Word 文档添加 XMLNode 控件](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [如何：将架构映射到 Visual Studio 内部的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
