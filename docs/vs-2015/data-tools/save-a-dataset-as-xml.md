---
title: 将数据集另存为 XML |Microsoft Docs
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
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e64c3c17934e5cdc5d6ca1f510c7164b86a77c1a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652862"
---
# <a name="save-a-dataset-as-xml"></a>将数据集另存为 XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过调用数据集上的可用 XML 方法来访问数据集中的 XML 数据。 若要以 XML 格式保存数据，可以调用 <xref:System.Data.DataSet> 的 <xref:System.Data.DataSet.GetXml%2A> 方法或 <xref:System.Data.DataSet.WriteXml%2A> 方法。

 调用 <xref:System.Data.DataSet.GetXml%2A> 方法将返回一个字符串，该字符串包含数据集中所有格式为 XML 的数据表中的数据。

 调用 <xref:System.Data.DataSet.WriteXml%2A> 方法会将 XML 格式的数据发送到您指定的文件。

### <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>将数据集中的数据以 XML 形式保存到变量

- @No__t_0 方法返回一个 <xref:System.String>。这意味着，你声明一个类型 <xref:System.String> 的变量，并为其分配 <xref:System.Data.DataSet.GetXml%2A> 方法的结果。

     [!code-csharp[VbRaddataSaving#12](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#12)]
     [!code-vb[VbRaddataSaving#12](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#12)]

### <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>将数据集中的数据以 XML 形式保存到文件中

- @No__t_0 方法有多个重载。 下面的代码演示如何将数据保存到文件。声明一个变量，并为其分配一个有效路径，以便将该文件保存到。

     [!code-csharp[VbRaddataSaving#13](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#13)]
     [!code-vb[VbRaddataSaving#13](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#13)]

## <a name="see-also"></a>请参阅
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
