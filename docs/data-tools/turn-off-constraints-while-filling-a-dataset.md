---
title: 在填充数据集时关闭约束
description: 了解如何在填充数据集时关闭约束。 以编程方式或通过使用数据集设计器挂起更新约束。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8a4d1e17d2f6a0159a9c0187d5e1a3d16216d0ba
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "94998312"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>在填充数据集时关闭约束

如果数据集包含约束 (如) 的外键约束，则它们可能会引发与针对数据集执行的操作顺序相关的错误。 例如，在加载相关的父记录之前加载子记录可能会违反约束并导致错误。 一旦加载子记录，约束就会检查相关的父记录，并引发错误。

如果没有允许临时约束挂起的机制，则每次尝试将记录加载到子表时都会引发错误。 挂起数据集中的所有约束的另一种方法是使用 <xref:System.Data.DataRow.BeginEdit%2A> 、和 <xref:System.Data.DataRow.EndEdit%2A> 属性。

> [!NOTE]
> 例如， <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 在关闭约束时，将不会引发验证事件 (例如，和) 。

## <a name="to-suspend-update-constraints-programmatically"></a>以编程方式暂停更新约束

- 下面的示例演示如何在数据集中暂时禁用约束检查：

     [!code-csharp[VbRaddataEditing#10](../data-tools/codesnippet/CSharp/turn-off-constraints-while-filling-a-dataset_1.cs)]
     [!code-vb[VbRaddataEditing#10](../data-tools/codesnippet/VisualBasic/turn-off-constraints-while-filling-a-dataset_1.vb)]

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>使用数据集设计器挂起更新约束

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅 [演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 在“属性”  窗口中，将 <xref:System.Data.DataSet.EnforceConstraints%2A> 属性设置为 `false`。

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
- [数据集中的关系](../data-tools/relationships-in-datasets.md)
