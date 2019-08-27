---
title: 在 WPF 应用程序中显示相关的数据 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e8a7bd540f5c8a99145b892d080d8cb54e57d968
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152123"
---
# <a name="display-related-data-in-wpf-applications"></a>在 WPF 应用程序中显示相关数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在某些应用程序，你可能想要使用来自多个表或相关对每个其他父-子关系中的实体的数据。 例如，你可能想要显示一个网格，其中显示从客户`Customers`表。 当用户选择某个特定客户时，另一个网格将显示该客户的相关订单`Orders`表。  
  
 可以创建数据绑定控件显示相关的数据，通过将项从**数据源**到 WPF 设计器窗口。  
  
## <a name="to-create-controls-that-display-related-records"></a>若要创建显示相关的记录的控件  
  
1. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口    。  
  
2. 单击“添加新数据源”，然后完成“数据源配置”向导   。  
  
3. 打开 WPF 设计器中，并确保该设计器包含有效的放置目标中的项的容器**数据源**窗口。  
  
     有关有效放置目标的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。  
  
4. 在中**数据源**窗口中，展开表示父表的节点或关系中的对象。 一个对多关系的"一"方上的父表或对象。  
  
5. 将父节点 （或任何单个项的父节点中） 从拖**数据源**窗口拖到设计器中的有效放置目标。  
  
     Visual Studio 生成创建拖动每个项的新数据绑定控件的 XAML。 XAML 还添加了一个新<xref:System.Windows.Data.CollectionViewSource>父表或对象的拖放目标资源。 对于某些数据源，Visual Studio 还会生成代码以将数据加载到父表或对象。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。  
  
6. 在中**数据源**窗口中，找到的相关的子表或对象。 相关的子表和对象显示为可展开节点的数据的父节点的列表底部。  
  
7. 将子节点 （或子节点中的任何单个项） 从拖**数据源**窗口拖到设计器中的有效放置目标。  
  
     Visual Studio 将生成为每个拖动的项创建新的数据绑定控件的 XAML。 XAML 还添加了一个新<xref:System.Windows.Data.CollectionViewSource>子表或对象的拖放目标资源。 这一新<xref:System.Windows.Data.CollectionViewSource>绑定到的父表或您刚刚拖动到设计器中的对象的属性。 对于某些数据源，Visual Studio 还会生成代码以将数据加载到子表或对象。  
  
     下图演示了相关**订单**表的**客户**表中的数据集中**数据源**窗口。  
  
     ![显示关系数据源窗口](../data-tools/media/datasources2.gif "DataSources2")  
  
## <a name="see-also"></a>请参阅  
 [将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)   
 [在 WPF 应用程序中创建查找表](../data-tools/create-lookup-tables-in-wpf-applications.md)   
 [演练：在 WPF 应用程序中显示相关的数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)
