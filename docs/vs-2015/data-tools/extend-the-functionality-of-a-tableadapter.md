---
title: 扩展 TableAdapter 的功能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- data [Visual Studio], extending TableAdapters
- TableAdapters, adding functionality
ms.assetid: 418249c8-c7f3-47ef-a94c-744cb6fe6aaf
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7e14acedeab457df10cc011a94f96d7202972eea
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697900"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>扩展 TableAdapter 的功能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将代码添加到 TableAdapter 的分部类文件扩展 TableAdapter 的功能。  
  
 中对 TableAdapter 进行任何更改时重新生成代码，用于定义 TableAdapter**数据集设计器**，或当向导修改 TableAdapter 的配置。 若要防止在 TableAdapter 的重新生成过程中删除你的代码，请将代码添加到 TableAdapter 的分部类文件。  
  
 分部类允许划分到多个物理文件的特定类代码。 有关详细信息，请参阅[分部](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448)或[分部 （类型）](https://msdn.microsoft.com/library/27320743-a22e-4c7b-b0b3-53afe3607334)。  
  
## <a name="locate-tableadapters-in-code"></a>在代码中查找 Tableadapter  
 Tableadapter 的设计时**数据集设计器**，生成的 TableAdapter 类不是嵌套的类的<xref:System.Data.DataSet>。 TableAdapter 位于基于 TableAdapter 关联数据集的名称的命名空间中。 例如，如果你的应用程序包含名为的数据集`HRDataSet`，Tableadapter 将位于`HRDataSetTableAdapters`命名空间。 (命名约定采用这种模式：*DatasetName* + `TableAdapters`)。  
  
 下面的示例假定名为 `CustomersTableAdapter` 的 TableAdapter 与 `NorthwindDataSet` 一起位于项目中。  
  
#### <a name="to-create-a-partial-class-for-a-tableadapter"></a>若要为 TableAdapter 创建分部类  
  
1. 将新类添加到你的项目，通过转到**项目**菜单并选择**添加类**。  
  
2. 将此类命名为 `CustomersTableAdapterExtended`。  
  
3. 选择“添加”。  
  
4. 该代码将替换为正确的命名空间和你的项目的分部类名称，如下所示：  
  
     [!code-csharp[VbRaddataTableAdapters#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/CustomersTableAdapterExtended.cs#2)]
     [!code-vb[VbRaddataTableAdapters#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/CustomersTableAdapterExtended.vb#2)]  
  
## <a name="see-also"></a>请参阅  
 [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
