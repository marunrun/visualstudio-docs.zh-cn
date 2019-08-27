---
title: 如何：以编程方式在特定文件夹内的搜索
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5ac3dbb169fee82a55cc41b773d3616c56f83534
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961896"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>如何：以编程方式在特定文件夹内的搜索
  此代码示例使用`Find`并`FindNext`方法中的电子邮件的主题字段中搜索文本**收件箱**。 此方法使用字符串筛选器为要检查的起始字母的字母 T`Subject`文本。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_SearchFolder#1](../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs#1)]

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
