---
title: Browse and Select a .NET Type Dialog Box | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d8e25ad181202a2c7994c116e2220426ca3d8509
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297613"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>“浏览并选择 .NET 类型”对话框
In the **Properties** window, dialog boxes, or designers such as the variable designer, when you select **Browse for Types…** from a list of data types, is the **Browse and Select a .NET Type** dialog box (referred to in an abbreviated form as the “type browser”). 在此对话框中，可以从程序集和项目的树视图中选择类型。

 在很多用户方案中都使用此对话框，这些方案包括：

- 设置变量或参数的类型时。

- 为一般活动选择类型时。

- 在 <xref:System.Activities.Statements.TryCatch> 活动上添加一个 catch 时。

> [!NOTE]
> 类型浏览器可以显示 Visual Basic 交错数组类型，但不显示多维数组类型。 See [Jagged Arrays](https://go.microsoft.com/fwlink/?LinkId=195226) and [Multidimensional Arrays](https://go.microsoft.com/fwlink/?LinkId=195227) for details.

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

#### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

1. In the **Type Name** box, enter the name of the type that you want to use.

2. 执行以下操作之一：

    - Once the name of the type that you want to use appears in the tree in the **Type Name** box, double-click the type to select it.

    - Type enough characters in the **Type Name** box to uniquely identify the type that you want to use and then press enter to select the type

#### <a name="to-select-a-generic-type-from-the-type-browser"></a>从类型浏览器中选择一个泛型类型

1. In the **Type Name** box, type in the name of the type that you want to use.

2. Once the name of the type that you want to use appears in the tree in the **Type Name** box, click the type to select it to cause drop-down boxes appear.

     Select the type that you want to use to close the generic from the drop-down boxes, and then click **OK**.

## <a name="types-displayed-in-the-type-browser"></a>类型浏览器中显示的类型
 类型浏览器中显示的类型可能因启动类型浏览器的方式而有所不同。 If the type browser was launched from a workflow project inside of **vs2010**, by default all of the types in the referenced assemblies and referenced projects are shown. If the type browser was launched from outside of a **vs2010** project system (such as in a rehosted workflow application or in a standalone workflow file), then by default the types from all of the assemblies loaded in the AppDomain are shown.

 可以按活动设计器开发人员筛选类型浏览器中的类型。 对于任何给定的活动，您可能只看到一个类型子集。 例如，在 <xref:System.Activities.Statements.TryCatch> 活动中，只有从 <xref:System.Exception> 派生的类型显示在类型浏览器中。

## <a name="filtering-search-results-in-the-type-browser"></a>在类型浏览器中筛选搜索结果
 The list of types in the **Type Name** box gets shorter as you type more characters to find a match. 只有其完全限定名以您键入的字符串开头的类型或者其简短名称以您键入的字符串开头的类型会显示在筛选出的列表中。

 例如:

1. Typing **Operation** matches <xref:System.OperationCanceledException> but not <xref:System.InvalidOperationException>. 若要匹配 <xref:System.InvalidOperationException>，请开始键入 System.I 或 Invalid。

2. Typing **Generic** matches <xref:System.GenericUriParser> but not types in the <xref:System.Collections.Generic> namespace. 若要在 <xref:System.Collections.Generic> 命名空间中搜索类型，请键入该命名空间的完全限定名称。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>使用类型浏览器对话框选择服务协定
 选择服务协定类型时，类型浏览器只显示具有 <xref:System.ServiceModel.ServiceContractAttribute> 特性的类型。

## <a name="see-also"></a>请参阅
 [使用活动设计器](../workflow-designer/using-the-activity-designers.md)