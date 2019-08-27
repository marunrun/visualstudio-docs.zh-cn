---
title: 如何：在受密码保护的文档中缓存数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c231aac3b78ddb5100cc06600059045fdc463e51
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826740"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>如何：在受密码保护的文档中缓存数据
  如果将数据添加到文档或使用密码保护的工作簿中的数据缓存，不会自动保存对缓存数据的更改。 通过重写在项目中的两种方法，可以将更改保存到缓存的数据。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>在 Word 文档中缓存

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>在使用密码保护的 Word 文档中缓存数据

1. 在`ThisDocument`类中，标记的公共字段或属性缓存。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

2. 重写<xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A>中的方法`ThisDocument`类，并从文档中删除保护。

     保存文档后，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]调用此方法来为您提供机会来取消保护文档。 这允许缓存的数据要保存更改。

3. 重写<xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A>中的方法`ThisDocument`类，并对文档重新应用保护。

     保存文档后，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]调用此方法使您可以对文档重新应用保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在使用密码保护的 Word 文档中缓存数据。 代码将删除在保护之前<xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A>方法，它将保存当前<xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A>值，以便可以在重新应用相同的保护类型<xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A>方法。

 [!code-csharp[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs#1)]
 [!code-vb[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb#1)]

### <a name="compile-the-code"></a>编译代码
 添加到此代码`ThisDocument`在项目中的类。 此代码假定该密码存储在名为`securelyStoredPassword`。

## <a name="cache-in-excel-workbooks"></a>在 Excel 工作簿中缓存
 在 Excel 项目中，此过程是必需仅当通过保护使用密码对整个工作簿时<xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A>方法。 此过程不是必需的如果使用保护仅使用密码的特定工作表<xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A>方法。

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>在使用密码保护的 Excel 工作簿中缓存数据

1. 在中`ThisWorkbook`类或某个`Sheet` *n*类中，标记的公共字段或属性缓存。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

2. 重写<xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A>中的方法`ThisWorkbook`类，并从该工作簿中删除保护。

     保存该工作簿后，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]调用此方法来使您可以取消保护工作簿。 这允许缓存的数据要保存更改。

3. 重写<xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A>中的方法`ThisWorkbook`类，并对文档重新应用保护。

     保存工作簿后，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]调用此方法使您可以对该工作簿重新应用保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在使用密码保护的 Excel 工作簿中缓存数据。 代码将删除在保护之前<xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A>方法，它将保存当前<xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A>并<xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A>值，以便可以在重新应用相同的保护类型<xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A>方法。

 [!code-vb[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs#1)]

### <a name="compile-the-code"></a>编译代码
 添加到此代码`ThisWorkbook`在项目中的类。 此代码假定该密码存储在名为`securelyStoredPassword`。

## <a name="see-also"></a>请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：脱机时或者在服务器上缓存数据以供使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式缓存中的 Office 文档的数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
