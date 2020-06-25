---
title: 添加到设计器中的对象使用不同的数据连接
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 38fa361536f9e99c013f9a13330fe1a68e53641a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281404"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>要添加到设计器中的对象使用的数据连接与设计器不同

要添加到设计器中的对象使用的数据连接与设计器当前所用的数据连接不同。 是否要替换设计器使用的连接?

在将项添加到**对象关系设计器**（**O/R 设计器**）时，所有项都使用一个共享数据连接。 （设计图面表示 <xref:System.Data.Linq.DataContext> ，它对图面上的所有对象使用单个连接。）如果将对象添加到使用的数据连接与设计器当前所用的数据连接不同的设计器，则会显示此消息。 若要解决此错误，可以选择保持现有连接。 如果选择这样做，则不会添加所选对象。 您也可以选择添加对象并将 <xref:System.Data.Linq.DataContext> 连接重置为新的连接。

## <a name="connection-options"></a>连接选项

- 若要将现有连接替换为所选对象使用的连接，请单击 **"是"**。

   所选对象将添加到**O/R 设计器**中，并且*DataContext*设置为新连接。

   > [!NOTE]
   > 如果单击 **"是**"，则**O/R 设计器**上的所有实体类都将映射到新连接。

- 若要继续使用现有连接并取消添加所选对象，请单击 "**否**"。

   操作被取消。 *DataContext*仍设置为现有连接。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
