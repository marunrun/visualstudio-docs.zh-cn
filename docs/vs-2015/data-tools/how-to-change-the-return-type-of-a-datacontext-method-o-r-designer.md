---
title: 如何：更改 DataContext 方法的返回类型（O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: c5b66bff-6dbb-43c0-bffa-317133ca5b9e
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 351a2f53d8ad8c5f29821d905c292cd988390869
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658844"
---
# <a name="how-to-change-the-return-type-of-a-datacontext-method-or-designer"></a>如何：更改 DataContext 方法的返回类型（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

根据在 <xref:System.Data.Linq.DataContext>中放置存储过程或函数的位置不同，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 方法（基于该存储过程或函数创建）的返回类型也有所不同。 如果直接将项放置在现有实体类上，则将创建具有该实体类返回类型的 <xref:System.Data.Linq.DataContext> 方法（如果该存储过程或函数返回的数据架构与实体类的形状相匹配）。 如果将项放在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]的空白区域，则将创建返回自动生成类型的 <xref:System.Data.Linq.DataContext> 方法。 在将 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格后可以更改该方法的返回类型。 若要检查或更改 <xref:System.Data.Linq.DataContext> 方法的返回类型，请选中该方法并在“属性”窗口中单击“返回类型”属性。

> [!NOTE]
> 不能使用“属性”窗口将返回类型设置为实体类的 <xref:System.Data.Linq.DataContext> 方法恢复为返回自动生成类型。 若要将 <xref:System.Data.Linq.DataContext> 方法恢复为返回自动生成类型，您必须将原始数据库对象再次拖动到 O/R 设计器上。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-change-the-return-type-of-a-datacontext-method-from-the-auto-generated-type-to-an-entity-class"></a>将 DataContext 方法的返回类型从自动生成类型更改为实体类

1. 在方法窗格中选择该 <xref:System.Data.Linq.DataContext> 方法。

2. 在“属性”窗口中选择“返回类型”，然后从“返回类型”列表中选择一个可用的实体类。 如果列表中没有您需要的实体类，可将该实体类添加到列表中，或在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中创建该实体类并将其添加到列表中。

3. 保存 .dbml 文件。

### <a name="to-change-the-return-type-of-a-datacontext-method-from-an-entity-class-back-to-the-auto-generated-type"></a>将 DataContext 方法的返回类型从实体类重新更改为自动生成类型

1. 在方法窗格中选择该 <xref:System.Data.Linq.DataContext> 方法并删除该方法。

2. 将数据库对象从**服务器资源管理器**/**数据库资源管理器**拖到 O/R 设计器的空白区域。

3. 保存 .dbml 文件。

## <a name="see-also"></a>请参阅
 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [DataContext 方法（o/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md) [如何：创建映射到存储过程和函数的 DataContext 方法（o/r 设计器）](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
