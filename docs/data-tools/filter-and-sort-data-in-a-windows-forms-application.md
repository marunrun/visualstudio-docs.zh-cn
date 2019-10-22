---
title: 在 Windows 窗体应用程序中对数据进行筛选和排序
ms.date: 11/04/2016
ms.topic: conceptual
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 68adaf6df9f97bee94e7cb393fa01ee133444c80
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648458"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>在 Windows 窗体应用程序中对数据进行筛选和排序

可以通过将 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性设置为返回所需记录的字符串表达式来筛选数据。

可以通过将 <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性设置为要排序的列名称对数据进行排序;追加 `DESC` 以便按降序排序，或者追加 `ASC` 以升序排序。

> [!NOTE]
> 如果你的应用程序不使用 <xref:System.Windows.Forms.BindingSource> 组件，则可以使用 <xref:System.Data.DataView> 对象对数据进行筛选和排序。 有关详细信息，请参阅[dataview](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews)。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件筛选数据

- 将 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性设置为要返回的表达式。 例如，以下代码返回 `CompanyName` 以 "B" 开头的客户：

     [!code-csharp[VbRaddataDisplaying#6](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_1.cs)]
     [!code-vb[VbRaddataDisplaying#6](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_1.vb)]

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件对数据进行排序

- 将 <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性设置为要作为排序依据的列。 例如，以下代码将按降序对 `CompanyName` 列中的客户排序：

     [!code-csharp[VbRaddataDisplaying#7](../data-tools/codesnippet/CSharp/filter-and-sort-data-in-a-windows-forms-application_2.cs)]
     [!code-vb[VbRaddataDisplaying#7](../data-tools/codesnippet/VisualBasic/filter-and-sort-data-in-a-windows-forms-application_2.vb)]

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)