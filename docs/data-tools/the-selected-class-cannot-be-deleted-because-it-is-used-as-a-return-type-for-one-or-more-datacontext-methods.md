---
title: 无法删除所选类，因为该类用作一个或多个 DataContext 方法的返回类型
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3b577dc32a233d1f18518aa27001f340c634314c
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65458174"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>无法删除所选类，因为该类用作一个或多个 DataContext 方法的返回类型

一个或多个 <xref:System.Data.Linq.DataContext> 方法的返回类型是所选实体类。 删除用作返回类型的实体类<xref:System.Data.Linq.DataContext>方法将导致项目无法编译。 若要删除选定的实体类，请找出使用该类的 <xref:System.Data.Linq.DataContext> 方法并将这些方法的返回类型设置为其他实体类。

若要将 <xref:System.Data.Linq.DataContext> 方法的返回类型恢复为原始自动生成类型，请首先从方法窗格中删除该 <xref:System.Data.Linq.DataContext> 方法，然后再次将该对象从“服务器资源管理器”/“数据库资源管理器”拖动到 O/R 设计器上。

## <a name="to-correct-this-error"></a>更正此错误

1. 通过在方法窗格中选择 <xref:System.Data.Linq.DataContext> 方法并在“属性”窗口中检查“返回类型”属性，可以确定使用该实体类作为返回类型的 <xref:System.Data.Linq.DataContext> 方法。

2. 将“返回类型”设置为其他实体类，或从方法窗格中删除该 <xref:System.Data.Linq.DataContext> 方法。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)