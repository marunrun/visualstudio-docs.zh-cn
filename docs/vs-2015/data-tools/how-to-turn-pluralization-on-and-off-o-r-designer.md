---
title: 如何：打开和关闭复数形式（O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: afe8c8a4429efb83c09d80a5dd00dfe08b0d63e3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665931"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：启用和禁用复数形式（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，当你将名称以 s 结尾或来自**服务器资源管理器**/**数据库资源管理器**的数据库对象拖动到[Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，生成的实体类的名称将从复数改为单数. 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将 Customers 表添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]将声称名为 Customer 的实体类，因为该类将仅为一个客户保存数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中展开“数据库工具”。

> [!NOTE]
> 如果“数据库工具”节点不可见，请选择“显示所有设置”。

1. 单击“O/R 设计器”。

2. 将**复数形式的名称**设置为 "**已启用**"  = **False** ，将 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 设置为，以便它不会更改类名称。

3. 将**复数形式的名称**设置为 "**已启用**"  = **True** ，以便将复数形式规则应用于添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 的对象的类名。

## <a name="see-also"></a>请参阅
 [Visual studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)在[visual studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
