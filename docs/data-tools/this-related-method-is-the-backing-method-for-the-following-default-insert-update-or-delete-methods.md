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
ms.openlocfilehash: a5ae70462079589ba2b63ee50cf0b7a0570e056a
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65457856"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>此相关方法是以下默认插入、更新或删除方法的支持方法

此相关方法是以下默认的备份方法`Insert`， `Update`，或`Delete`方法。 如果删除这些方法，则备份方法也将被删除。 是否要继续?

所选`DataContext`方法当前用作之一`Insert`， `Update`，或`Delete`方法的一个实体类上**O/R 设计器**。 删除所选的方法使实体类，则使用此方法以还原为默认运行时行为的执行插入、 更新或删除在更新过程。

## <a name="selected-method-options"></a>所选的方法选项

- 若要删除所选的方法，使实体类使用运行时的更新，请单击**是**。

   所选方法将被删除，并且使用此方法重写更新行为的所有类将还原为使用默认 LINQ to SQL 运行时行为。

- 若要关闭消息框中，不对所选的方法保持不变，请单击**否**。

   消息框关闭，不进行任何更改。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)