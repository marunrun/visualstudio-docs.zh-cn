---
title: 此相关方法是以下默认插入、更新或删除方法的支持方法
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 11c5c7d3c8078aa420074e9e32bb132489b169c8
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252948"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>此相关方法是以下默认插入、更新或删除方法的支持方法

此相关方法是以下默认`Insert`、 `Update`或`Delete`方法的后备方法。 如果删除这些方法，则备份方法也将被删除。 是否要继续?

所选`DataContext`方法当前用作**O/R 设计器**上`Update`某个实体`Delete`类的`Insert`、或方法之一。 删除所选方法会导致使用此方法的实体类恢复为在更新过程中执行插入、更新或删除操作的默认运行时行为。

## <a name="selected-method-options"></a>选择的方法选项

- 若要删除所选方法，使实体类使用运行时更新，请单击 **"是"** 。

   将删除所选方法，并使用默认的 LINQ to SQL 运行时行为将使用此方法替代更新行为的任何类还原为。

- 若要关闭该消息框，使所选方法保持不变，请单击 "**否**"。

   消息框关闭，不进行任何更改。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)