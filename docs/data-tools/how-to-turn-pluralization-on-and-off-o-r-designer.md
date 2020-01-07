---
title: 如何：启用和禁用复数形式（O-R 设计器）
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 54b3376f9388116f179e2b09bcd136a37f3029f5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586440"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：启用和禁用复数形式（O/R 设计器）
默认情况下，当您将名称以 s 或从**服务器资源管理器**结束或从**数据库资源管理器**结束的数据库对象拖动到[Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，所生成的实体类的名称将从复数改为单数形式。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，将 `Customers` 表添加到**O/R 设计器**将生成一个名为 `Customer` 的实体类，因为该类只保存单个客户的数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中展开“数据库工具”。

    > [!NOTE]
    > 如果“数据库工具”节点不可见，请选择“显示所有设置”。

3. 单击“O/R 设计器”。

4. 将**复数形式的名称**设置为 "**启用**" = **False** ，以设置**O/R 设计器**，使其不更改类名称。

5. 将**复数形式的名称**设置为 "**已启用**" = **True** ，以便将复数形式规则应用于添加到**O/R 设计器**的对象的类名。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
