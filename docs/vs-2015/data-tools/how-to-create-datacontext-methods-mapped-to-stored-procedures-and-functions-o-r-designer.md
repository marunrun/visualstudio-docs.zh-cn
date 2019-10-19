---
title: 如何：创建映射到存储过程和函数的 DataContext 方法（O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70053b74a4dd2ad569e1e8195f4c9b2e7b214440
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665977"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>如何：创建映射到存储流程和函数的 DataContext 方法（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将存储过程和函数作为 <xref:System.Data.Linq.DataContext> 方法添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 中。 调用该方法并传入所需参数将对数据库运行存储过程或函数，并返回 <xref:System.Data.Linq.DataContext> 方法的返回类型的数据。 有关 <xref:System.Data.Linq.DataContext> 方法的详细信息，请参阅[DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

> [!NOTE]
> 将更改从实体类保存到数据库时，还可以使用存储过程重写执行插入、更新和删除操作的默认 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时行为。 有关详细信息，请参阅[如何：分配存储过程以执行更新、插入和删除（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="creating-datacontext-methods"></a>创建 DataContext 方法
 您可以通过将存储过程或函数从**服务器资源管理器/数据库资源管理器**拖到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 来创建 <xref:System.Data.Linq.DataContext> 方法。

> [!NOTE]
> 根据在 <xref:System.Data.Linq.DataContext>上放置存储过程或函数的位置不同，生成的 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 方法的返回类型也有所不同。 如果直接将项放置在现有实体类上，则将创建具有该实体类返回类型的 <xref:System.Data.Linq.DataContext> 方法。 如果将项放在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]的空白区域，则将创建返回自动生成类型的 <xref:System.Data.Linq.DataContext> 方法。 在将 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格后可以更改该方法的返回类型。 若要检查或更改 <xref:System.Data.Linq.DataContext> 方法的返回类型，请选中该方法并在“属性”窗口中检查“返回类型”属性。 有关详细信息，请参阅[如何：更改 DataContext 方法的返回类型（O/R 设计器）](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>创建返回自动生成类型的 DataContext 方法

1. 在**服务器资源管理器**/**数据库资源管理器**中，展开您正在使用的数据库的 "**存储过程**" 节点。

2. 找到所需的存储过程并将其拖到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]的空白区域。

     具有自动生成返回类型的 <xref:System.Data.Linq.DataContext> 方法即被创建，并出现在“方法”窗格中。

#### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>创建具有实体类的返回类型的 DataContext 方法

1. 在**服务器资源管理器**/**数据库资源管理器**中，展开您正在使用的数据库的 "**存储过程**" 节点。

2. 找到所需的存储过程并将其拖到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中的一个现有实体类上。

     具有所选实体类的返回类型的 <xref:System.Data.Linq.DataContext> 方法即被创建，并出现在“方法”窗格中。

> [!NOTE]
> 有关更改返回类型的现有<xref:System.Data.Linq.DataContext>方法，请参阅[如何：更改 DataContext 方法的返回类型（O/R 设计器）](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)。

## <a name="see-also"></a>请参阅
 Visual Studio [DataContext 方法（o/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md) [中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[演练：创建 LINQ to SQL 类（o-r 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [介绍 linq in Visual Basic](https://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984) [如何：编写 linq 查询C#](https://msdn.microsoft.com/library/45e47fcc-cfa1-4b72-b161-d038ae87bd23)
