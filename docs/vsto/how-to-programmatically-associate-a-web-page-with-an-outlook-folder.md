---
title: 如何：以编程方式将网页与 Outlook 文件夹关联
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: b8d44ffc46557243d2681b8f8b4a3b85d1cd9be6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546141"
---
# <a name="how-to-programmatically-associate-a-web-page-with-an-outlook-folder"></a>如何：以编程方式将网页与 Outlook 文件夹关联
  此示例 `HtmlView` 在 Microsoft Office Outlook 中检查名为的文件夹。 如果该文件夹不存在，则代码会创建该文件夹并向其分配网页。 如果该文件夹存在，则代码将显示文件夹内容。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_HTMLFolder#1](../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs#1)]

## <a name="see-also"></a>另请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)
