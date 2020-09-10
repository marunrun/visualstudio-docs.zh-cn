---
title: 无法删除所选的类
description: 无法删除所选类，因为该类用作一个或多个 DataContext 方法的返回类型
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 84fabc7f0f1efdf06006597aec9bb813578589a8
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743248"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>无法删除所选类，因为该类用作一个或多个 DataContext 方法的返回类型

一个或多个 <xref:System.Data.Linq.DataContext> 方法的返回类型是所选实体类。 删除用作方法的返回类型的实体类 <xref:System.Data.Linq.DataContext> 会导致项目的编译失败。 若要删除选定的实体类，请找出使用该类的 <xref:System.Data.Linq.DataContext> 方法并将这些方法的返回类型设置为其他实体类。

若要将 <xref:System.Data.Linq.DataContext> 方法的返回类型恢复为原始自动生成类型，请首先从方法窗格中删除该 <xref:System.Data.Linq.DataContext> 方法，然后再次将该对象从“服务器资源管理器”/“数据库资源管理器”拖动到 O/R 设计器上****************。

## <a name="to-correct-this-error"></a>更正此错误

1. 通过在方法窗格中选择 <xref:System.Data.Linq.DataContext> 方法并在“属性”窗口中检查“返回类型”属性，可以确定使用该实体类作为返回类型的 <xref:System.Data.Linq.DataContext> 方法************。

2. 将“返回类型”设置为其他实体类，或从方法窗格中删除该 <xref:System.Data.Linq.DataContext> 方法****。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
