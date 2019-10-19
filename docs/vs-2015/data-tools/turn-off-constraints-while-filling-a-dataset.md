---
title: 在填充数据集时关闭约束 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6646f669bf2c465d8e0f705f8fba956b979952ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667167"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>在填充数据集时关闭约束
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果数据集包含约束（例如，外键约束），则 theycan 会引发与针对数据集执行的操作顺序相关的错误。 例如，在 loadingrelated 的父记录之前加载子记录可能会违反约束并导致错误。 一旦加载子记录，约束就会检查相关的父记录，并引发错误。

 如果没有允许临时约束挂起的机制，则每次尝试将记录加载到子表时都会引发错误。 挂起数据集中的所有约束的另一种方法是使用 <xref:System.Data.DataRow.BeginEdit%2A>，并 <xref:System.Data.DataRow.EndEdit%2A> 属性。

> [!NOTE]
> 关闭约束时，将不会引发验证事件（例如 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging>）。

### <a name="to-suspend-update-constraints-programmatically"></a>以编程方式暂停更新约束

- 下面的示例演示如何在数据集中暂时禁用约束检查：

     [!code-csharp[VbRaddataEditing#10](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#10)]
     [!code-vb[VbRaddataEditing#10](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#10)]

### <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>使用数据集设计器挂起更新约束

1. 在数据集设计器中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。

2. 在“属性” 窗口中，将 <xref:System.Data.DataSet.EnforceConstraints%2A> 属性设置为 `false`。

## <a name="see-also"></a>请参阅
 使用[数据集中](../data-tools/relationships-in-datasets.md)[的 tableadapter 关系填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
