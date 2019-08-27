---
title: 以编程方式缓存 Office 文档中的数据源
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
ms.openlocfilehash: 5e63b478fb16965f639a76dad0cbc3b2715bc7e2
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401403"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>如何：以编程方式缓存中的 Office 文档的数据源
  你可以以编程方式将数据对象添加到文档中的数据缓存通过调用`StartCaching`方法的主机项，如<xref:Microsoft.Office.Tools.Word.Document>， <xref:Microsoft.Office.Tools.Excel.Workbook>，或<xref:Microsoft.Office.Tools.Excel.Worksheet>。 从数据缓存中删除数据对象，通过调用`StopCaching`宿主项的方法。

 `StartCaching`方法和`StopCaching`方法都是私有的但它们在 IntelliSense 中显示。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 当你使用`StartCaching`方法将数据对象添加到数据缓存中，数据对象不需要使用声明<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>属性。 但是，数据对象必须满足某些要求，若要添加到数据缓存中。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

## <a name="to-programmatically-cache-a-data-object"></a>若要以编程方式缓存数据对象

1. 声明在类级别，不在方法中的数据对象。 此示例假定你将声明<xref:System.Data.DataSet>名为`dataSet1`你想要以编程方式缓存。

     [!code-csharp[Trin_VstcoreDataExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#12)]
     [!code-vb[Trin_VstcoreDataExcel#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#12)]

2. 实例化数据对象，然后调用`StartCaching`方法文档或工作表的实例并传入的数据对象的名称。

     [!code-csharp[Trin_VstcoreDataExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#13)]
     [!code-vb[Trin_VstcoreDataExcel#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#13)]

## <a name="to-stop-caching-a-data-object"></a>若要停止缓存数据对象

1. 调用`StopCaching`方法文档或工作表的实例并传入的数据对象的名称。 此示例假定你拥有<xref:System.Data.DataSet>名为`dataSet1`想要停止缓存。

     [!code-csharp[Trin_VstcoreDataExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#14)]
     [!code-vb[Trin_VstcoreDataExcel#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#14)]

    > [!NOTE]
    > 不要调用`StopCaching`的事件处理程序从`Shutdown`事件的文档或工作表。 按时间`Shutdown`引发事件，它太迟是若要修改的数据缓存。 有关详细信息`Shutdown`事件，请参阅[Events in Office Projects](../vsto/events-in-office-projects.md)。

## <a name="see-also"></a>请参阅

- [缓存数据](../vsto/caching-data.md)
- [如何：脱机时或者在服务器上缓存数据以供使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/saving-data.md)
