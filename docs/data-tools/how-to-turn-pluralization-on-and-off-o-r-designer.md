---
title: 如何：打开和关闭复数形式（O-R 设计器）
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 769d1760692cad6a6b813ece16d69f4abd3d26b1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402784"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>如何：打开和关闭复数形式（O/R 设计器）
默认情况下，当您拖放以 s 或 ies 从结尾的数据库对象**服务器资源管理器**或**数据库资源管理器**拖到[Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)、生成的实体类的名称从复数形式更改为单数形式。 这样可以更准确地表示实例化的实体类映射到单个数据记录的事实。 例如，添加`Customers`到表**O/R 设计器**导致一个名为的实体类`Customer`因为该类将仅为一个客户保存数据。

> [!NOTE]
> 默认情况下，复数形式仅在 Visual Studio 的英语版本中启用。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>打开和关闭复数形式

1. 在 **“工具”** 菜单上，单击 **“选项”**。

2. 在“选项”对话框中展开“数据库工具”。

    > [!NOTE]
    > 如果“数据库工具”节点不可见，请选择“显示所有设置”。

3. 单击“O/R 设计器”。

4. 设置**名称的复数形式**到**已启用** = **False**设置**O/R 设计器**，以便它不会更改类名称.

5. 设置**名称的复数形式**到**已启用** = **True**若要添加到的对象的类名称应用复数规则**O/R设计器**。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)