---
title: 添加到设计器的对象使用不同的数据连接
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c85e0c17eeb4cfbd786faac338c8b908c5a7f363
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260929"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>要添加到设计器中的对象使用不同的数据连接与设计器

要添加到设计器中的对象使用的数据连接与设计器当前所用的数据连接不同。 是否要替换设计器使用的连接?

添加到的项时**对象关系设计器**(**O/R 设计器**)，所有项都使用同一个共享的数据连接。 （设计图面表示 <xref:System.Data.Linq.DataContext>，它将单个连接用于图面上的所有对象。）如果添加到设计器中的对象使用的数据连接与设计器当前使用的数据连接不同，则会出现此消息。 若要解决此错误，可以选择保持现有连接。 如果选择这样做，则不会添加所选对象。 您也可以选择添加对象并将 <xref:System.Data.Linq.DataContext> 连接重置为新的连接。

## <a name="connection-options"></a>连接选项

- 若要将所选对象使用的连接替换为现有连接，请单击**是**。

   所选的对象添加到**O/R 设计器**，并*DataContext.Connection*设置为新的连接。

   > [!NOTE]
   > 如果单击**是**，所有实体都类上**O/R 设计器**映射到新的连接。

- 若要继续使用现有连接并添加所选的对象的取消，单击**否**。

   操作被取消。 DataContext.Connection 仍然设置为现有连接  。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
