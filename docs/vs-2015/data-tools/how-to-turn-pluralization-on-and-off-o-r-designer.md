---
title: 如何：打开和关闭复数形式设计器)  (Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665931"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：启用和禁用复数形式（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，当您将名称以 s 结尾或从**服务器资源管理器**数据库资源管理器结束的数据库对象拖动 / **Database Explorer**到[Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，所生成的实体类的名称将从复数改为单数形式。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将 Customers 表添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]将声称名为 Customer 的实体类，因为该类将仅为一个客户保存数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在“工具”  菜单上，单击“选项” 。

2. 在“选项”对话框中展开“数据库工具”********。

> [!NOTE]
> 如果“数据库工具”节点不可见，请选择“显示所有设置”********。

1. 单击“O/R 设计器”****。

2. 将 "**名称" 的复数形式****设置为**  =  "**False** " 可将设置为， [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 以便它不会更改类名称。

3. 将**复数形式的名称**设置**为 "**  =  **True** " 可将复数形式规则应用到添加到中的对象的类名 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

## <a name="see-also"></a>另请参阅
 [Visual studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)在 [visual studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
