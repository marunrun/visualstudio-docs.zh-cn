---
title: 如何：以编程方式搜索特定联系人
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Outlook 中搜索特定联系人。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6813a137558a245c66d4b24deac07b1a6a77796a
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524605"
---
# <a name="how-to-programmatically-search-for-a-specific-contact"></a>如何：以编程方式搜索特定联系人
  此示例按姓氏和名称在 Outlook 联系人文件夹中搜索特定联系人。 该示例假定联系人文件夹中存在名为 **John Evans** 的联系人。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_Outlook_RL_SearchForContact#1](../vsto/codesnippet/CSharp/trin_outlook_rl_searchforcontact/thisaddin.cs#1)]
 [!code-vb[Trin_Outlook_RL_SearchForContact#1](../vsto/codesnippet/VisualBasic/trin_outlook_rl_searchforcontact/thisaddin.vb#1)]

## <a name="see-also"></a>另请参阅
- [处理联系人项](../vsto/working-with-contact-items.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
