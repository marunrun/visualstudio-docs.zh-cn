---
title: 将数据集另存为 XML
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3c993ac8703468a24a99e114563fec1bdc817581
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566223"
---
# <a name="save-a-dataset-as-xml"></a>将数据集另存为 XML

通过在数据集上调用提供的 XML 方法访问 XML 数据集中的数据。 若要以 XML 格式保存数据，您可以调用<xref:System.Data.DataSet.GetXml%2A>方法或<xref:System.Data.DataSet.WriteXml%2A>方法的<xref:System.Data.DataSet>。

调用<xref:System.Data.DataSet.GetXml%2A>方法返回一个字符串，包含格式为 XML 在数据集中的所有数据表中的数据。

调用<xref:System.Data.DataSet.WriteXml%2A>方法将 XML 格式的数据发送到你指定的文件。

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>若要在数据集中的数据以 XML 形式保存到变量

- <xref:System.Data.DataSet.GetXml%2A> 方法返回 <xref:System.String>。 声明类型的变量<xref:System.String>并将其分配的结果<xref:System.Data.DataSet.GetXml%2A>方法。

     [!code-vb[VbRaddataSaving#12](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_1.vb)]
     [!code-csharp[VbRaddataSaving#12](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_1.cs)]

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>若要将数据集中的数据以 XML 形式保存到文件

- <xref:System.Data.DataSet.WriteXml%2A>方法有若干重载。 声明一个变量并将其分配有效的路径保存到文件。 下面的代码演示如何将数据保存到文件：

     [!code-vb[VbRaddataSaving#13](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_2.vb)]
     [!code-csharp[VbRaddataSaving#13](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_2.cs)]

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)