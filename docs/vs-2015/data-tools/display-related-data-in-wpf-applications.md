---
title: 在 WPF 应用程序中显示相关数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 3aa80194-0191-474d-9d28-5ec05654b426
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6efa79fc59ed9812cf6162096dd462100b71fbca
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672413"
---
# <a name="display-related-data-in-wpf-applications"></a>在 WPF 应用程序中显示相关数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在某些应用程序中，你可能想要处理来自多个表或实体的数据，这些表或实体在父子关系中相互相关。 例如，你可能想要显示一个网格，该网格显示 `Customers` 表中的客户。 当用户选择特定客户时，另一个网格会显示相关 `Orders` 表中该客户的订单。

 可以通过将项从 "**数据源**" 窗口拖到 WPF 设计器来创建显示相关数据的数据绑定控件。

## <a name="to-create-controls-that-display-related-records"></a>创建显示相关记录的控件

1. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口。

2. 单击“添加新数据源”，然后完成“数据源配置”向导。

3. 打开 WPF 设计器，确保设计器包含一个容器，该容器是 "**数据源**" 窗口中项的有效拖放目标。

     有关有效放置目标的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

4. 在 "**数据源**" 窗口中，展开表示关系中的父表或对象的节点。 父表或对象位于一对多关系的 "一" 端。

5. 将父节点（或父节点中的任何单个项）从 "**数据源**" 窗口拖到设计器中的有效放置目标。

     Visual Studio 将生成 XAML，为拖动的每个项创建新的数据绑定控件。 XAML 还会将父表或对象的新 <xref:System.Windows.Data.CollectionViewSource> 添加到拖放目标的资源。 对于某些数据源，Visual Studio 还会生成代码，以便将数据加载到父表或对象。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

6. 在 "**数据源**" 窗口中，找到相关的子表或对象。 相关的子表和对象在父节点的数据列表底部显示为可扩充节点。

7. 将子节点（或子节点中的任何单个项）从 "**数据源**" 窗口拖到设计器中的有效放置目标。

     Visual Studio 将生成 XAML，为拖动的每个项创建新的数据绑定控件。 XAML 还会将子表或对象的新 <xref:System.Windows.Data.CollectionViewSource> 添加到拖放目标的资源。 此新 <xref:System.Windows.Data.CollectionViewSource> 绑定到刚拖到设计器中的父表或对象的属性。 对于某些数据源，Visual Studio 还会生成代码，以便将数据加载到子表或对象。

     下图演示了 "**数据源**" 窗口中的数据集的 " **Customers** " 表的相关 " **Orders** " 表。

     ![显示关系的 "数据源" 窗口](../data-tools/media/datasources2.gif "DataSources2")

## <a name="see-also"></a>请参阅
 [将 wpf 控件绑定到 Visual studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)[将 wpf 控件绑定到 visual studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)中的数据在[wpf 应用程序中创建查找表](../data-tools/create-lookup-tables-in-wpf-applications.md)[演练：在 wpf 应用程序中显示相关数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)
