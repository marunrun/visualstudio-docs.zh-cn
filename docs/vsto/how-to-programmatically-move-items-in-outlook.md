---
title: 如何：以编程方式在 Outlook 中移动项
description: 了解如何以编程方式在 Microsoft Outlook 中移动项。 此示例将收件箱中的未读电子邮件移动到名为 Test 的文件夹中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], moving items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b247df68827767a53d8d066f4750dfa9da52ac7
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525566"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>如何：以编程方式在 Outlook 中移动项
  此示例将 **收件箱** 中的未读电子邮件移动到名为 **Test** 的文件夹中。 此示例仅移动字段中包含单词 **Test** 的消息 `Subject` 。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_MoveItems#1](../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 名为 **Test** 的 Outlook 邮件文件夹。

- 一封电子邮件，它在字段中使用字词 **Test** `Subject` 。

## <a name="see-also"></a>另请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式在特定文件夹中搜索](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [如何：在收到电子邮件时以编程方式执行操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
