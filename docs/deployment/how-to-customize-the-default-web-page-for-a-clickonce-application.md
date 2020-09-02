---
title: 自定义 ClickOnce 应用程序的默认网页
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish.htm Web page
- ClickOnce deployment default Web page
- deploying applications [ClickOnce], publishing
- publishing, ClickOnce
ms.assetid: 418de18c-bee9-4f24-9cd9-0252d175070d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ee4c1211840f17afe371961dea644372cd63efb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85382466"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>如何：自定义 ClickOnce 应用程序的默认网页
将 ClickOnce 应用程序发布到 Web 时，将自动生成一个网页，并随应用程序一起发布。 默认页面包含应用程序的名称和用于安装应用程序的链接、安装必备组件或访问 MSDN 上的帮助。

> [!NOTE]
> 您在页面上看到的实际链接取决于查看该页的计算机以及所包含的先决条件。

 网页的默认名称为 *Publish.htm*;您可以在 " **项目设计器**" 中更改该名称。 有关详细信息，请参阅 [如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)。

 仅当检测到较新的版本时，才会发布 *Publish.htm* 网页。

> [!NOTE]
> 对 **发布** 设置所做的更改不会影响 *Publish.htm* 页面，但有一种情况例外：如果在最初发布后添加或删除先决条件，则先决条件列表将不再准确。 需要为必备链接编辑文本，以反映所做的更改。

### <a name="to-customize-the-publish-web-page"></a>自定义发布网页

1. 将 ClickOnce 应用程序发布到 Web 位置。 有关详细信息，请参阅 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

2. 在 Web 服务器上，在 Visual Web Designer 或其他 HTML 编辑器中打开 *Publish.htm* 文件。

3. 根据需要自定义页面并保存。

4. 可选。 若要防止 Visual Studio 覆盖自定义的发布网页，请取消选中 "**发布选项**" 对话框中的 "**每次发布后自动生成部署**网页"。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：将必备组件与 ClickOnce 应用程序一起安装](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)