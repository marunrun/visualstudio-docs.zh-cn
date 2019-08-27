---
title: 如何：以编程方式将网页与 Outlook 文件夹相关联
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- folders [Office development in Visual Studio], Web pages and
- Outlook [Office development in Visual Studio], Web pages attached to folders
- Web pages [Office development in Visual Studio], Outlook folders
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e83f8b7f6bcdb790b5e545aa76426bc05f0735f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817304"
---
# <a name="how-to-programmatically-associate-a-web-page-with-an-outlook-folder"></a>如何：以编程方式将网页与 Outlook 文件夹相关联
  此示例检查名为`HtmlView`Microsoft Office Outlook 中。 如果文件夹不存在，代码会创建该文件夹，并为其分配到 Web 页。 如果该文件夹存在，代码将显示该文件夹的内容。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_HTMLFolder#1](../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs#1)]

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)
