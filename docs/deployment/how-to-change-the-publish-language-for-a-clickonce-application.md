---
title: 发布 ClickOnce 应用程序的语言更改
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e80a65b65d75d925decdf60b633a7d51ea9bafce
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263178"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>如何：更改 ClickOnce 应用程序的发布语言

发布时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序中，在安装到的语言和开发计算机的区域性的默认设置过程中显示的用户界面。 如果发布已本地化的应用程序，需要指定语言和区域性的本地化的版本匹配。 这由`Publish language`为你的项目的属性。

`Publish language`属性可以设置**发布选项**对话框中，可通过访问**发布**页**项目设计器**。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="to-change-the-publish-language"></a>若要更改发布语言

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**选项**按钮以打开**发布选项**对话框。

4. 单击**说明**。

5. 在中**发布选项**对话框框中，选择一种语言和区域性从**发布语言**下拉列表，再单击**确定**。

## <a name="see-also"></a>请参阅

- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)