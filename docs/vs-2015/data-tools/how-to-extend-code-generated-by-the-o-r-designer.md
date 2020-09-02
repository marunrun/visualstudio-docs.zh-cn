---
title: 如何：扩展由 O R 设计器生成的代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1d60090ca16907e16bb58970d793124c5bb2dec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665948"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>如何：扩展 O/R 设计器生成的代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在更改设计器图面上的实体类和其他对象时，将重新生成由 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]生成的代码。 当设计器重新生成代码时，你添加到生成的代码中的任何代码一般都会被重新声称的代码覆盖。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]提供了一种生成分部类文件的功能，您可以将代码添加到分部类文件中而不会被覆盖。 将你自己的代码添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]生成的代码中的一个示例是在 LINQ to SQL（实体）类中添加数据验证。 有关信息，请参阅 [如何：向实体类添加验证](../data-tools/how-to-add-validation-to-entity-classes.md)。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="adding-code-to-an-entity-class"></a>向实体类中添加代码

#### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>创建分部类并向实体类中添加代码

1. 在中打开或创建一个新的 LINQ to SQL 类文件 (**.dbml** 文件) [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。  (在**解决方案资源管理器**数据库资源管理器中双击 **.dbml**文件 / **Database Explorer**。 ) 

2. 在中 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ，右键单击要为其添加验证的类，然后单击 " **查看代码**"。

     将打开代码编辑器，其中显示所选实体类的分部类。

3. 在该实体类的分部类声明中添加您的代码。

## <a name="adding-code-to-a-datacontext"></a>向 DataContext 中添加代码

#### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>创建分部类并向 DataContext 中添加代码

1. 在中打开或创建一个新的 LINQ to SQL 类文件 (**.dbml** 文件) [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。  (在**解决方案资源管理器**数据库资源管理器中双击 **.dbml**文件 / **Database Explorer**。 ) 

2. 在中 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ，右键单击设计器上的空白区域，然后单击 " **查看代码**"。

     将打开代码编辑器，其中显示 DataContext 的分部类。

3. 在 DataContext 的分部类声明中添加您的代码。

## <a name="see-also"></a>另请参阅
 [LINQ to SQL Visual Studio 中的工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[演练：创建 LINQ to SQL 类 (O R 设计器) ](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [演练：向实体类添加验证](https://msdn.microsoft.com/library/85b06a02-b2e3-4534-95b8-d077c8d4c1d7)
