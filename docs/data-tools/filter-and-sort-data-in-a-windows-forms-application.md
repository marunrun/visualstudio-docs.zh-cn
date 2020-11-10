---
title: 在 Windows 窗体应用程序中对数据进行筛选和排序
description: 在 Windows 窗体应用程序中对数据进行筛选和排序。 将 "筛选器" 属性设置为一个字符串表达式，该表达式返回所需的记录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 076ec70fa3a2aed3ddc65d0a4b50272c824a1cfb
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94435060"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>在 Windows 窗体应用程序中对数据进行筛选和排序

您可以通过将属性设置 <xref:System.Windows.Forms.BindingSource.Filter%2A> 为返回所需记录的字符串表达式来筛选数据。

您可以通过将属性设置 <xref:System.Windows.Forms.BindingSource.Sort%2A> 为要排序的列名称对数据进行排序; 追加 `DESC` 以降序排序，或按 `ASC` 升序排序。

> [!NOTE]
> 如果你的应用程序不使用 <xref:System.Windows.Forms.BindingSource> 组件，则可以使用对象对数据进行筛选和排序 <xref:System.Data.DataView> 。 有关详细信息，请参阅 [dataview](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews)。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件筛选数据

- 将 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性设置为要返回的表达式。 例如，以下代码将返回以 `CompanyName` "B" 开头的的客户：

     [!code-csharp[VbRaddataDisplaying#6](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_1.cs)]
     [!code-vb[VbRaddataDisplaying#6](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_1.vb)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件对数据进行排序

- 将 <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性设置为要作为排序依据的列。 例如，下面的代码对列中的客户按 `CompanyName` 降序排序：

     [!code-csharp[VbRaddataDisplaying#7](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_2.cs)]
     [!code-vb[VbRaddataDisplaying#7](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_2.vb)]

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
