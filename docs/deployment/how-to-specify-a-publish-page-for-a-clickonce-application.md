---
title: 如何-指定 ClickOnce 应用程序的发布页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying publish page
- Publish Page property
- publishing, ClickOnce
- ClickOnce deployment, specifying publish page
ms.assetid: 9d70eebb-bdee-4b42-8e7e-7a07e199bdf7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: acf7178a6b5456d048421533b8497682d69c2ee0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381959"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的发布页
发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，将生成一个默认网页（publish.htm），并随应用程序一起发布。 此页包含应用程序的名称、安装应用程序的链接和/或任何系统必备组件，并链接到描述的帮助主题 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 您的项目的 "**发布页**" 属性允许您为应用程序指定网页的名称 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

 指定发布页面后，下一次发布时，它将复制到发布位置;如果再次发布，则不会被覆盖。 如果希望自定义页面外观，可以这样做，而不必担心会丢失所做的更改。 有关详细信息，请参阅[如何：自定义 ClickOnce 默认](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)网页。

 可以在 "**发布选项**" 对话框中设置 "**发布页**" 属性，该对话框可从 "**项目设计器**" 的 "**发布**" 窗格中访问。

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>指定 ClickOnce 应用程序的自定义网页

1. 在**解决方案资源管理器**中选择一个项目后，在 "**项目**" 菜单上单击 "**属性**"。

2. 选择 "**发布**" 窗格。

3. 单击 "**选项**" 按钮打开 "**发布选项**" 对话框。

4. 单击“部署”。****

5. 在 "**发布选项**" 对话框中，确保已选中 "**发布后打开部署**网页" 复选框（默认情况下应选中）。

6. 在 "**部署 web 页**" 框中，输入网页的名称，然后单击 **"确定"**。

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>若要防止每次发布时启动发布页

1. 在**解决方案资源管理器**中选择一个项目后，在 "**项目**" 菜单上单击 "**属性**"。

2. 选择 "**发布**" 窗格。

3. 单击 "**选项**" 按钮打开 "**发布选项**" 对话框。

4. 单击“部署”。****

5. 在 "**发布选项**" 对话框中，清除 "**发布后打开部署**网页" 复选框。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：自定义 ClickOnce 的默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)