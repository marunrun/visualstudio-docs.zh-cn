---
title: 在 Windows 窗体应用程序中的筛选器和排序数据 |Microsoft Docs
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
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e12ee25225cb294565490c4d46f26618958dfdf6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697876"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>在 Windows 窗体应用程序中对数据进行筛选和排序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

设置筛选数据<xref:System.Windows.Forms.BindingSource.Filter%2A>属性设置为一个字符串表达式，返回所需的记录。  
  
 对数据进行排序通过设置<xref:System.Windows.Forms.BindingSource.Sort%2A>想要按其排序的列名称的属性; 追加`DESC`按降序排序，还是追加`ASC`以按升序排序。  
  
> [!NOTE]
> 如果你的应用程序不使用<xref:System.Windows.Forms.BindingSource>组件，您可以筛选和排序数据使用<xref:System.Data.DataView>对象。 有关详细信息，请参阅[Dataview](https://msdn.microsoft.com/library/0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b)。  
  
## <a name="to-filter-data-by-using-a-bindingsource-component"></a>通过使用 BindingSource 组件来筛选数据  
  
- 设置<xref:System.Windows.Forms.BindingSource.Filter%2A>属性设置为你想要返回的表达式。 例如，以下代码将返回与客户`CompanyName`"B"开头的：  
  
     [!code-csharp[VbRaddataDisplaying#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#6)]
     [!code-vb[VbRaddataDisplaying#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#6)]  
  
## <a name="to-sort-data-by-using-a-bindingsource-component"></a>若要使用 BindingSource 组件对数据进行排序  
  
- 设置<xref:System.Windows.Forms.BindingSource.Sort%2A>属性设置为你想要按其排序的列。 例如，下面的代码对客户排序上`CompanyName`降序排序的列：  
  
     [!code-csharp[VbRaddataDisplaying#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#7)]
     [!code-vb[VbRaddataDisplaying#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#7)]  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
