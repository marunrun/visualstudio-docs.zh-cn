---
title: 数据类继承 （O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f2c1f5328abd8ea814e1175b17129dd8a89040ef
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697934"
---
# <a name="data-class-inheritance-or-designer"></a>数据类继承（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

像其他对象一样，[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 类可以使用继承，并可从其他类派生。 在代码中，可以通过声明一个类继承自另一个类来指定对象间的继承关系。 在数据库中，可通过多种方式创建继承关系。 [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)]（[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]）支持通常在关系系统中实现的单表继承概念。  
  
 在单表继承中，一个数据库表同时包含基类和派生类的列。 使用关系数据时，一个鉴别器列包含的值确定任意给定的记录属于哪个类。 例如，考虑一个包含公司所有员工的 Persons 表。 一些人是员工，一些人是经理。 Persons 表包含一个名为 Type 的列，该列用值 1 表示经理，用值 2 表示员工。 Type 列是鉴别器列。 在此方案中，可以创建一个员工子类，并仅使用 Type 值为 2 的记录来填充该类。  
  
 使用 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 配置实体类中的继承时，将包含继承数据的单表两次拖动到设计器上：一次拖动对应继承层次结构中的一个类。 将表添加到设计器后，从“对象关系设计器”工具箱中用“继承”项连接这些表，然后在“属性”窗口中设置四个继承属性。  
  
## <a name="inheritance-properties"></a>继承属性  
 下表列出了这些继承属性及其说明：  
  
|属性|描述|  
|--------------|-----------------|  
|鉴别器属性|决定当前记录所属的类的属性，该属性映射到列。|  
|基类鉴别器值|决定记录所属的基类的值，该值位于指定为鉴别器属性的列中。|  
|派生类鉴别器值|决定记录所属的派生类的值，该值位于指定为鉴别器属性的属性中。|  
|继承默认值|属性中的值指定为时，应进行填充的类**鉴别器属性**不匹配**基类鉴别器值**或**派生的类鉴别器值**。|  
  
 创建一个使用继承并对应于关系数据的对象模型可能有些不易理解。 本主题提供了有关配置继承时所需的基本概念及各个属性的信息。 下列主题对如何使用 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]配置继承进行了更清楚的阐释。  
  
|主题|描述|  
|-----------|-----------------|  
|[如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|描述如何使用 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]配置使用单表继承的实体类。|  
|[演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|提供有关如何使用 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]配置使用单表继承的实体类的分步说明。|  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [演练：创建 LINQ to SQL 类 （O-R 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [演练：通过使用单表继承 （O/R 设计器） 中创建 LINQ to SQL 类](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)   
 [入门](https://msdn.microsoft.com/library/db8a557a-fef8-4f4f-bb91-8cff7250ee25)
