---
title: 如何：应用程序和部署清单重新签名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d5956ad23fe22c7c36b712fac61df268586142df
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697558"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>如何：对应用程序和部署清单重新签名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对 Windows 窗体应用程序、 Windows Presentation Foundation 应用程序 (xbap) 或 Office 解决方案的应用程序清单中的部署属性进行更改后，必须重新签名的应用程序和部署清单与证书。 此过程有助于确保不会在最终用户计算机上安装经过篡改的文件。  
  
 你的客户想要为应用程序签名和部署清单具有自己的证书时可能会重新对清单签名的另一种情况。  
  
## <a name="re-signing-the-application-and-deployment-manifests"></a>重新对应用程序和部署清单进行签名  
 此过程假定您已对你的应用程序清单文件 (.manifest) 中做出了更改。 有关详细信息，请参阅[如何：更改部署属性](https://msdn.microsoft.com/66052a3a-8127-4964-8147-2477ef5d1472)。  
  
#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 重新签名的应用程序和部署清单  
  
1. 打开**Visual Studio 命令提示符**窗口。  
  
2. 将目录更改为包含要签名的清单文件的文件夹。  
  
3. 键入以下命令以登录应用程序清单文件。 ManifestFileName 替换为你的清单文件扩展名的名称。 证书替换为证书文件的相对或完全限定路径和密码替换为证书的密码。  
  
    ```  
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     例如，可以运行以下命令以登录为外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单。 Visual Studio 创建的临时证书不建议以部署到生产环境中。  
  
    ```  
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
4. 键入以下命令以更新并对签名部署清单文件，替换占位符名称，如在上一步中所示。  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     例如，可以运行以下命令以更新和 Excel 外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序部署清单进行签名。  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5. （可选） 将复制的主部署清单 (发布\\*appname*.application) 到你的版本部署目录 (publish\Application 文件\\*appname*_*版本*)。  
  
## <a name="updating-and-re-signing-the-application-and-deployment-manifests"></a>更新和重新签名的应用程序和部署清单进行签名  
 此过程假定您已更改应用程序清单文件 (.manifest)，但有其他文件进行了更新。 当文件更新时，也必须更新表示的文件的哈希。  
  
#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 更新和重新签名的应用程序和部署清单  
  
1. 打开**Visual Studio 命令提示符**窗口。  
  
2. 将目录更改为包含要签名的清单文件的文件夹。  
  
3. 从发布输出文件夹中的文件中删除.deploy 文件扩展名。  
  
4. 键入以下命令以使用更新后的文件的新哈希更新应用程序清单和应用程序清单文件进行签名。 ManifestFileName 替换为你的清单文件扩展名的名称。 证书替换为证书文件的相对或完全限定路径和密码替换为证书的密码。  
  
    ```  
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     例如，可以运行以下命令以登录为外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单。 Visual Studio 创建的临时证书不建议以部署到生产环境中。  
  
    ```  
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5. 键入以下命令以更新并对签名部署清单文件，替换占位符名称，如在上一步中所示。  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     例如，可以运行以下命令以更新和 Excel 外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序部署清单进行签名。  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
6. 将.deploy 文件扩展名添加到文件，但应用程序和部署清单文件。  
  
7. （可选） 将复制的主部署清单 (发布\\*appname*.application) 到你的版本部署目录 (publish\Application 文件\\*appname*_*版本*)。  
  
## <a name="see-also"></a>请参阅  
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce 和验证码](../deployment/clickonce-and-authenticode.md)   
 [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)   
 [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)   
 [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [如何：调试具有受限权限的 ClickOnce 应用程序](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [如何：为 ClickOnce 应用程序添加到客户端计算机的受信任的发行者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)
