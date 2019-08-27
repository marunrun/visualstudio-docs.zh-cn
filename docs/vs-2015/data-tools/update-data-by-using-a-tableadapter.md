---
title: 使用 TableAdapter 更新数据 |Microsoft Docs
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
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 30d1fd3ee211d6b30f435104a2e2f9b42ed100c0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692348"
---
# <a name="update-data-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在数据集中的数据已修改并验证后，可以将更新后的数据发送回 databaseby 调用`Update`TableAdapter 的方法。 `Update`方法更新单个数据表，并运行基于的正确命令 （INSERT、 UPDATE 或 DELETE）<xref:System.Data.DataRow.RowState%2A>的表中每个数据行。 时数据集具有相关表，Visual Studio 生成一个 TableAdapterManager 类，用于执行更新操作。 TableAdapterManager 类可确保按正确的顺序基于数据库中定义的外键约束进行更新。 当您使用数据绑定控件时，数据绑定体系结构将创建调用 tableAdapterManager TableAdapterManager 类的一个成员变量。 有关详细信息，请参阅[分层更新概述](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)。  
  
> [!NOTE]
> 当您尝试使用数据集的内容更新数据源时，你会遇到错误。若要避免错误，我们建议将调用该适配器的代码放在随时`Update`方法内的`try` / `catch`块。  
  
 更新数据源的确切步骤可以根据业务需求而有所不同，但包括以下步骤：  
  
1. 调用该适配器`Update`中的方法`try` / `catch`块。  
  
2. 如果捕获到异常，找到导致此错误的数据行。 有关详细信息，请参阅[如何：查找具有错误的行](https://msdn.microsoft.com/library/1fa907c5-fe66-4f29-a253-2b97b900050c)。  
  
3. 解决此问题在数据行 （您可以如果以编程方式或无效的行显示给用户进行修改），并再试一次更新 (<xref:System.Data.DataRow.HasErrors%2A>， <xref:System.Data.DataTable.GetErrors%2A>)。  
  
## <a name="savedata-to-a-database"></a>Savedata 到数据库  
 调用`Update`TableAdapter 的方法。 传递包含要写入到数据库的值的数据表的名称。  
  
#### <a name="to-update-a-database-by-using-a-tableadapter"></a>若要使用 TableAdapter 更新数据库  
  
- 将 TableAdapter`Update`中的方法`try` / `catch`块。 下面的示例演示如何更新的内容`Customers`表中`NorthwindDataSet`内`try` / `catch`块。  
  
     [!code-csharp[VbRaddataSaving#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#9)]
     [!code-vb[VbRaddataSaving#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#9)]  
  
## <a name="see-also"></a>请参阅  
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
