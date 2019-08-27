---
title: 如何：以编程方式将文本文件打开为工作簿
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening text files as
- text [Office development in Visual Studio], text files
- text files, opening as workbooks
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 61e51f6274bc22ed0d34d33f5ff85bfbfbd927bd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812451"
---
# <a name="how-to-programmatically-open-text-files-as-workbooks"></a>如何：以编程方式将文本文件打开为工作簿
  为工作簿，可以打开一个文本文件。 您必须传递你想要打开的文本文件的名称。 可以指定几个可选参数，例如，要从哪一行开始分析以及文件中的数据的列格式。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#80)]
 [!code-vb[Trin_VstcoreExcelAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#80)]

## <a name="compile-the-code"></a>编译代码
 此示例需要以下组件：

- 名为的逗号分隔的文本文件`Test.txt`，其中包含至少三行文本。

- 该文本文件`Test.txt`要存储在驱动器 c。

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [如何：以编程方式创建新的工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
