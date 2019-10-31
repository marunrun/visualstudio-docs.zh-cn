---
title: 以编程方式在 Office 文档中缓存数据源
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- StartCaching method
- data caching [Office development in Visual Studio], programmatically
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 241ce42c2d411fdaf611f3a7f2b52eb40c8c32a2
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189578"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>如何：以编程方式在 Office 文档中缓存数据源
  可以通过调用主机项的 `StartCaching` 方法（如 <xref:Microsoft.Office.Tools.Word.Document>、<xref:Microsoft.Office.Tools.Excel.Workbook>或 <xref:Microsoft.Office.Tools.Excel.Worksheet>），以编程方式将数据对象添加到文档中的数据缓存。 通过调用主机项的 `StopCaching` 方法，从数据缓存中删除数据对象。

 `StartCaching` 方法和 `StopCaching` 方法均为私有方法，但它们显示在 IntelliSense 中。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 当使用 `StartCaching` 方法将数据对象添加到数据缓存时，不需要使用 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性声明数据对象。 但是，数据对象必须满足某些要求才能添加到数据缓存中。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

## <a name="to-programmatically-cache-a-data-object"></a>以编程方式缓存数据对象

1. 在类级别（而不是在方法中）声明数据对象。 此示例假设要声明一个要以编程方式缓存的名为 `dataSet1` 的 <xref:System.Data.DataSet>。

     [!code-csharp[Trin_VstcoreDataExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#12)]
     [!code-vb[Trin_VstcoreDataExcel#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#12)]

2. 实例化数据对象，然后调用文档或工作表实例的 `StartCaching` 方法，并传入数据对象的名称。

     [!code-csharp[Trin_VstcoreDataExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#13)]
     [!code-vb[Trin_VstcoreDataExcel#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#13)]

## <a name="to-stop-caching-a-data-object"></a>停止缓存数据对象

1. 调用文档或工作表实例的 `StopCaching` 方法，并传入数据对象的名称。 此示例假设你有一个要停止缓存的名为 `dataSet1` 的 <xref:System.Data.DataSet>。

     [!code-csharp[Trin_VstcoreDataExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#14)]
     [!code-vb[Trin_VstcoreDataExcel#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#14)]

    > [!NOTE]
    > 不要从文档或工作表的 `Shutdown` 事件的事件处理程序调用 `StopCaching`。 在引发 `Shutdown` 事件时，修改数据缓存的时间太晚。 有关 `Shutdown` 事件的详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

## <a name="see-also"></a>请参阅

- [缓存数据](../vsto/caching-data.md)
- [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/save-data-back-to-the-database.md)
