---
title: 如何：指定最终用户将从安装的位置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3139cb337428dfc0c14e5bae47e682ce169bc81d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159124"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>如何：指定最终用户从中进行安装的位置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

发布时[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序中，用户可以下载和安装应用程序的位置不一定是最初在其中发布应用程序的位置。 例如，在某些组织中开发人员可能会发布到暂存服务器，应用程序，然后管理员将移动应用程序到 Web 服务器。  
  
 在这种情况下，可以使用`Installation URL`属性来指定用户将可以下载应用程序的 Web 服务器。 这是必需的以便应用程序清单知道在何处查找更新。  
  
 `Installation URL`属性可以设置上**发布**页**项目设计器**。  
  
 **请注意**`Installation URL`也可以使用设置属性**发布向导**。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。  
  
### <a name="to-specify-an-installation-url"></a>若要指定安装 URL  
  
1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。  
  
2. 单击“发布”选项卡  。  
  
3. 在安装 URL 字段中，输入使用完全限定的 URL 使用以下格式的安装位置 http://www.microsoft.com/ApplicationName ，或使用以下格式的 UNC 路径\\ \Server\ApplicationName。  
  
## <a name="see-also"></a>请参阅  
 [如何：指定 Visual Studio 复制文件的位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
