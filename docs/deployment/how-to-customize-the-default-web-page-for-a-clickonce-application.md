---
title: 自定义 ClickOnce 应用程序的默认网页
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 66d304be4e2435b6ec1ecafe8aeb473b83fa1033
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263334"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>如何：自定义 ClickOnce 应用程序的默认网页
在发布 ClickOnce 应用程序到 Web，Web 页自动生成并随应用程序一起发布。 默认页包含的应用程序和用于安装应用程序、 安装必备组件，或访问 MSDN 上的帮助链接的名称。

> [!NOTE]
> 在页看到的实际链接取决于计算机页查看位置以及要包括的先决条件。

 Web 页面的默认名称是*Publish.htm*; 你可以在名称**项目设计器**。 有关详细信息，请参阅[如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)。

 *Publish.htm*发布网页时，仅当检测到较新版本。

> [!NOTE]
> 对所做的更改你**发布**设置不会影响*Publish.htm*页上，有一个例外： 如果添加或删除系统必备组件在最初发布后，将系统必备组件的列表不再是准确的。 你将需要编辑的先决条件的链接，以反映所做的更改的文本。

### <a name="to-customize-the-publish-web-page"></a>若要自定义 Web 发布页

1. 发布 ClickOnce 应用程序到 Web 位置。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

2. 在 Web 服务器上，打开*Publish.htm* Visual Web 设计器或另一个 HTML 编辑器中的文件。

3. 自定义为所需的页，并将其保存。

4. 可选。 若要阻止 Visual Studio 覆盖您自定义的发布的网页，取消选中**自动生成部署网页后每个发布**中**发布选项**对话框。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：与 ClickOnce 应用程序安装的必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)