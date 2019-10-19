---
title: 无法删除所选类，因为它用作一个或多个 DataContext 方法的返回类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cf16fe7453388e19308ed603ee9dbbac207cec41
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667254"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>无法删除所选类，因为该类用作一个或多个 DataContext 方法的返回类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一个或多个 <xref:System.Data.Linq.DataContext> 方法的返回类型是所选实体类。 删除用作 <xref:System.Data.Linq.DataContext> 方法返回类型的实体类将导致项目编译失败。 若要删除选定的实体类，请找出使用该类的 <xref:System.Data.Linq.DataContext> 方法并将这些方法的返回类型设置为其他实体类。

 若要将 <xref:System.Data.Linq.DataContext> 方法的返回类型还原为其最初自动生成的类型，请首先从 "方法" 窗格中删除 <xref:System.Data.Linq.DataContext> 方法，然后将该对象从**服务器资源管理器**/**数据库资源管理器**重新拖到 O/R 设计器上。

### <a name="to-correct-this-error"></a>更正此错误

1. 通过在方法窗格中选择 <xref:System.Data.Linq.DataContext> 方法并在 "**属性**" 窗口中检查 "**返回类型**" 属性，确定使用实体类作为返回类型的 <xref:System.Data.Linq.DataContext> 方法。

2. 将“返回类型”设置为其他实体类，或从方法窗格中删除该 <xref:System.Data.Linq.DataContext> 方法。

## <a name="see-also"></a>请参阅
 [LINQ to SQL Visual Studio 中的工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[演练：创建 LINQ to SQL 类（o-r 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [DataContext 方法（o/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md) [如何：更改 DataContext 方法的返回类型（O/r 设计器）](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)
