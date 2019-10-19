---
title: 要添加到设计器中的对象使用的数据连接与设计器当前使用的不同。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9ec76446aff930475ea5e3ca0133e11b3798b0c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672291"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer-is-currently-using"></a>您添加到设计器的对象使用与当前使用的设计器不同的数据连接
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要添加到设计器中的对象使用的数据连接与设计器当前所用的数据连接不同。 是否要替换设计器使用的连接?

 在将项添加到[!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)]（[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]）时，所有项都使用同一个共享数据连接。 （设计图面表示 <xref:System.Data.Linq.DataContext>，它对图面上的所有对象使用单个连接。）如果将对象添加到使用的数据连接与设计器当前所用的数据连接不同的设计器，则会显示此消息。 若要解决此错误，可以选择保持现有连接。 如果选择这样做，则不会添加所选对象。 您也可以选择添加对象并将 <xref:System.Data.Linq.DataContext> 连接重置为新的连接。

> [!NOTE]
> 如果单击 **"是**"，则 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 上的所有实体类都将映射到新连接。

### <a name="to-replace-the-existing-connection-with-the-connection-used-by-the-selected-object"></a>将现有连接替换为所选对象使用的连接

- 单击“是”。

     所选对象将添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中，并且 DataContext.Connection 设置为新连接。

### <a name="to-continue-to-use-the-existing-connection-and-cancel-adding-the-selected-object"></a>继续使用现有连接并取消添加所选对象的操作

- 单击“否”。

     操作被取消。 DataContext.Connection 仍然设置为现有连接。

## <a name="see-also"></a>请参阅
 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)