---
title: 如何：将复数化打开和关闭 （O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c8497f63e2b4dc51caa69b1babe0d707e8370aab
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704957"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：打开和关闭复数形式（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，当您拖放以 s 或 ies 从结尾的数据库对象**服务器资源管理器**/**数据库资源管理器**拖到[LINQ to SQL 工具在 Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)，生成的实体类的名称从复数形式更改为单数形式。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将 Customers 表添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]将声称名为 Customer 的实体类，因为该类将仅为一个客户保存数据。  
  
> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式  
  
1. 在 **“工具”** 菜单上，单击 **“选项”**。  
  
2. 在“选项”对话框中展开“数据库工具”。  
  
> [!NOTE]
> 如果“数据库工具”节点不可见，请选择“显示所有设置”。  
  
1. 单击“O/R 设计器”。  
  
2. 设置**名称的复数形式**到**已启用** = **False**设置[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]，以便它不会更改类名称。  
  
3. 设置**名称的复数形式**到**已启用** = **True**若要添加到的对象的类名称应用复数规则[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
