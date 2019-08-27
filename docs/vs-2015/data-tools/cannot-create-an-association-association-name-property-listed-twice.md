---
title: 无法创建关联&lt;关联名称&gt;-属性已列出两次 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 3ced8bda-210e-4caf-9d8f-96cdbba19251
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 257490a91ac21868be276cfc3ae5514222dae86d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703839"
---
# <a name="cannot-create-an-association-ltassociation-namegt---property-listed-twice"></a>无法创建关联 &lt;关联名称&gt; - 属性已列出两次
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

无法创建关联 \<关联名称>。 相同的属性已列出多次：\<属性名称>。  
  
 关联由在“关联编辑器”对话框中选择的“关联属性”定义。 对于关联中的每个类，属性只能列出一次。  
  
 消息中的属性在 Parent 类或 Child 类的“关联属性”中出现了多次。  
  
### <a name="to-resolve-this-condition"></a>解决此问题的方法  
  
- 检查消息并记下消息中指定的属性。  
  
- 单击“确定”，关闭该消息框。  
  
- 检查“关联属性”并移除重复项。  
  
- 单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](https://msdn.microsoft.com/library/a57e82d5-f7e4-4894-8add-3d9ba4fce186)   
 [如何：创建 LINQ to SQL 类 （O/R 设计器） 之间的关联 （关系）](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)   
 [演练：创建 LINQ to SQL 类 （O-R 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
