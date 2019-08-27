---
title: 如何：调试具有受限权限的 ClickOnce 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ClickOnce applications
- ClickOnce deployment, debugging
- ClickOnce applications, debugging
ms.assetid: 6991ea91-5253-451b-923d-22273a3d38b1
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d60f88c4d1532a03922f12f21bb9b455ef5d84d8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153801"
---
# <a name="how-to-debug-a-clickonce-application-with-restricted-permissions"></a>如何：使用受限权限对 ClickOnce 应用程序进行调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

作为开发人员，你很可能使用完全信任权限运行开发计算机，因此在调试 ClickOnce 应用程序时不会遇到最终用户在使用受限权限运行它时可能会遇到的相同安全异常。  
  
 为了捕获这些异常，你需要使用与最终用户相同的权限来调试应用程序。 可以在 **“项目设计器”** 的 **“安全”** 页上启用使用受限权限进行调试。  
  
 此外，在开发调用 Web 服务的应用程序时，这些 Web 服务通常驻留在开发计算机上。 部署之后，最终用户会通过其他 URL 访问这些 Web 服务。 若要在调试过程中模拟最终用户体验，可以指定一个 URL，调试器会如同从该 URL 调用 Web 服务一样来处理这些服务。  
  
### <a name="to-enable-debugging-with-restricted-permissions"></a>使用受限权限启用调试  
  
1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。  
  
2. 在“项目设计器”  中，单击“安全”  选项卡。  
  
3. 选中“启用 ClickOnce 安全设置”  复选框，然后单击“这是部分可信的应用程序”  选项按钮。  
  
4. 单击“高级”  按钮。  
  
5. 选中“使用选定权限集调试此应用程序”  复选框，然后单击“确定”  。  
  
     调试应用程序时，任何访问不属于权限集一部分的权限的尝试都会引发安全异常。  
  
### <a name="to-specify-a-url-for-debugging"></a>指定用于调试的 URL  
  
1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。  
  
2. 在“项目设计器”  中，单击“安全”  选项卡。  
  
3. 选中“启用 ClickOnce 安全设置”  复选框，然后单击“这是部分可信的应用程序”  选项按钮。  
  
4. 单击“高级”  按钮。  
  
5. 选中“使用选定权限集调试此应用程序”  复选框，然后单击“确定”  。  
  
6. 在“调试此应用程序，就如同它是从以下 URL 位置下载的一样”  文本框中，输入 URL 或网络路径。  
  
## <a name="see-also"></a>请参阅  
 [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)   
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
