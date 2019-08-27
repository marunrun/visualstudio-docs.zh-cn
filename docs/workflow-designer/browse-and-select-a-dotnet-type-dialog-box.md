---
title: 工作流设计器-浏览并选择.NET 类型对话框
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: f48a30e11e28daef2d1803646d2b495bcb718b84
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993182"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>“浏览并选择 .NET 类型”对话框

在中**属性**窗口、 对话框或如变量设计器中，当您选择的设计器**浏览类型**数据类型的列表，从是**浏览并选择.NET 类型**对话框中 （在"类型浏览器"以缩写形式称为）。 在此对话框中，可以从程序集和项目的树视图中选择类型。

在很多用户方案中都使用此对话框，这些方案包括：

- 设置变量或参数的类型时。

- 为一般活动选择类型时。

- 在 <xref:System.Activities.Statements.TryCatch> 活动上添加一个 catch 时。

> [!NOTE]
> 类型浏览器可以显示 Visual Basic 交错数组类型，但不显示多维数组类型。 请参阅[交错数组](http://go.microsoft.com/fwlink/?LinkId=195226)并[多维数组](http://go.microsoft.com/fwlink/?LinkId=195227)有关详细信息。

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

1. 在中**类型名称**框中，输入你想要使用的类型的名称。

2. 执行下列操作之一：

    - 当你想要使用的类型名称出现的树中后**类型名称**框中，双击该类型以选择它。

    - 键入在足够字符**类型名称**中，用于唯一标识你想要使用并按 enter 以选择的类型的类型

### <a name="to-select-a-generic-type-from-the-type-browser"></a>从类型浏览器中选择一个泛型类型

1. 在中**类型名称**框中，键入你想要使用的类型的名称。

2. 当你想要使用的类型名称出现的树中后**类型名称**框中，单击要选择它以导致下拉列表框的类型出现。

     选择想要用于关闭下拉列表框中，从泛型，然后单击类型**确定**。

## <a name="types-displayed-in-the-type-browser"></a>类型浏览器中显示的类型

类型浏览器中显示的类型可能因启动类型浏览器的方式而有所不同。 如果从工作流项目中的启动类型浏览器**vs2010**、 默认情况下，所有被引用程序集中的类型和显示引用的项目。 如果从外部的启动类型浏览器**vs2010**项目系统 （如重新承载工作流应用程序或独立工作流文件中），则默认情况下显示来自所有 AppDomain 中加载的程序集的类型.

可以按活动设计器开发人员筛选类型浏览器中的类型。 对于任何给定的活动，您可能只看到一个类型子集。 例如，在 <xref:System.Activities.Statements.TryCatch> 活动中，只有从 <xref:System.Exception> 派生的类型显示在类型浏览器中。

## <a name="filtering-search-results-in-the-type-browser"></a>在类型浏览器中筛选搜索结果

中的类型列表**类型名称**框就会越短键入更多字符可找到匹配项。 只有其完全限定名称以您键入的字符串开头的类型或其简短名称以您键入的字符串开头的类型出现在筛选后的列表。

例如：

1. 键入**操作**匹配<xref:System.OperationCanceledException>但不是<xref:System.InvalidOperationException>。 若要匹配 <xref:System.InvalidOperationException>，请开始键入 System.I 或 Invalid。

2. 键入**泛型**匹配<xref:System.GenericUriParser>但不是在类型<xref:System.Collections.Generic>命名空间。 若要搜索中的类型<xref:System.Collections.Generic>命名空间中，键入命名空间的完全限定的名称。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>使用类型浏览器对话框选择服务协定

选择服务协定类型时，类型浏览器只显示具有 <xref:System.ServiceModel.ServiceContractAttribute> 特性的类型。

## <a name="see-also"></a>请参阅

- [使用活动设计器](../workflow-designer/using-the-activity-designers.md)