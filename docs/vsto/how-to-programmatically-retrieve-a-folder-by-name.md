---
title: 如何：以编程方式按名称检索文件夹
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], retrieving by name
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a494f954f3f670fb796b33a0dbd01e2512ad1d26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955724"
---
# <a name="how-to-programmatically-retrieve-a-folder-by-name"></a>如何：以编程方式按名称检索文件夹
  此示例获取命名的自定义文件夹的引用，然后显示文件夹的内容。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_GetFolderName#1](../vsto/codesnippet/CSharp/Trin_OL_GetFolderName/thisaddin.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 名为 TestFolder 的文件夹。

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式在特定文件夹内的搜索](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [如何：以编程方式搜索特定联系人](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)
