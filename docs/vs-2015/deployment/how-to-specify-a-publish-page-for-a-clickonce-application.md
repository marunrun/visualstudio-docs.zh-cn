---
title: 如何：指定 ClickOnce 应用程序的发布页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 63356c6eb423ddead54290cc11c865a5102f55f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202160"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的发布页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

发布时[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，生成默认网页 (publish.htm) 并将其随应用程序一起发布。 此页包含的应用程序、 安装应用程序和/或任何系统必备组件的链接和帮助主题描述的链接名称[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]。 **发布页面**为你的项目的属性，可指定的 Web 页面的名称在[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。  
  
 后指定发布页下, 一次发布时，它会复制到发布位置;它不会再次发布如果被覆盖。 如果你想要自定义页面的外观，就可以做到而无需担心丢失所做的更改。 有关详细信息，请参阅[如何：自定义 ClickOnce 的默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)。  
  
 **发布页面**可以在属性设置**发布选项**对话框中，可通过访问**发布**窗格**项目设计器**.  
  
### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>若要指定一个 ClickOnce 应用程序的自定义 Web 页  
  
1. 在“解决方案资源管理器”  中选择一个项目，然后在“项目”  菜单上单击“属性”  。  
  
2. 选择**发布**窗格。  
  
3. 单击**选项**按钮以打开**发布选项**对话框。  
  
4. 单击**部署**。  
  
5. 在中**发布选项**对话框框中，请确保**发布后打开部署网页**复选框处于选中状态 （默认情况下应选择）。  
  
6. 在中**部署 web 页：** 框中，输入 Web 页的名称，然后单击**确定**。  
  
### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>若要防止每次发布的时启动发布页  
  
1. 在“解决方案资源管理器”  中选择一个项目，然后在“项目”  菜单上单击“属性”  。  
  
2. 选择**发布**窗格。  
  
3. 单击**选项**按钮以打开**发布选项**对话框。  
  
4. 单击**部署**。  
  
5. 在中**发布选项**对话框中，清除**发布后打开部署网页**复选框。  
  
## <a name="see-also"></a>请参阅  
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [如何：发布 ClickOnce 应用程序使用发布向导](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [如何：自定义 ClickOnce 默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)
