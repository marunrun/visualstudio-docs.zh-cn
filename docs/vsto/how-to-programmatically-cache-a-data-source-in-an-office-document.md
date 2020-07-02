---
title: 以编程方式在 Office 文档中缓存数据源
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 8ec3a38d109de561e3cba77951764dd8dd9479df
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544763"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>如何：以编程方式在 Office 文档中缓存数据源
  可以通过调用 `StartCaching` 主机项（如、或）的方法，以编程方式将数据对象添加到文档中的数据缓存 <xref:Microsoft.Office.Tools.Word.Document> <xref:Microsoft.Office.Tools.Excel.Workbook> <xref:Microsoft.Office.Tools.Excel.Worksheet> 。 通过调用主机项的方法，从数据缓存中删除数据对象 `StopCaching` 。

 `StartCaching`方法和方法都 `StopCaching` 是私有的，但它们显示在 IntelliSense 中。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 使用 `StartCaching` 方法将数据对象添加到数据缓存时，无需使用特性声明数据对象 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 。 但是，数据对象必须满足某些要求才能添加到数据缓存中。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

## <a name="to-programmatically-cache-a-data-object"></a>以编程方式缓存数据对象

1. 在类级别（而不是在方法中）声明数据对象。 此示例假设你要声明一个 <xref:System.Data.DataSet> 要以 `dataSet1` 编程方式缓存的名为的。

     [!code-csharp[Trin_VstcoreDataExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#12)]
     [!code-vb[Trin_VstcoreDataExcel#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#12)]

2. 实例化数据对象，然后调用 `StartCaching` 文档或工作表实例的方法，并传入数据对象的名称。

     [!code-csharp[Trin_VstcoreDataExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#13)]
     [!code-vb[Trin_VstcoreDataExcel#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#13)]

## <a name="to-stop-caching-a-data-object"></a>停止缓存数据对象

1. 调用 `StopCaching` 文档或工作表实例的方法，并传入数据对象的名称。 此示例假设你有一个 <xref:System.Data.DataSet> `dataSet1` 要停止缓存的命名。

     [!code-csharp[Trin_VstcoreDataExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#14)]
     [!code-vb[Trin_VstcoreDataExcel#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#14)]

    > [!NOTE]
    > 不要 `StopCaching` 从 `Shutdown` 文档或工作表的事件的事件处理程序调用。 `Shutdown`当引发事件时，修改数据缓存的时间太晚。 有关事件的详细信息 `Shutdown` ，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

## <a name="see-also"></a>请参阅

- [缓存数据](../vsto/caching-data.md)
- [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/save-data-back-to-the-database.md)
