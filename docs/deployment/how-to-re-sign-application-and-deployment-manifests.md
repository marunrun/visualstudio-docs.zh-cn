---
title: 如何：应用程序和部署清单重新签名 |Microsoft Docs
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e934832f20ea7ab11484cdeb345f989aa842e06d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928355"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>如何：对应用程序清单和部署清单重新签名
对 Windows 窗体应用程序、 Windows Presentation Foundation 应用程序 (xbap) 或 Office 解决方案的应用程序清单中的部署属性进行更改后，必须重新签名的应用程序和部署清单与证书。 此过程有助于确保不会在最终用户计算机上安装经过篡改的文件。

 你的客户想要为应用程序签名和部署清单具有自己的证书时可能会重新对清单签名的另一种情况。

## <a name="re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单重新签名
 此过程假定您已对你的应用程序清单文件中做出了更改 (*.manifest*)。 有关详细信息，请参阅[如何：更改部署属性](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472)。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 重新签名的应用程序和部署清单

1. 打开**Visual Studio 命令提示符**窗口。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 键入以下命令以登录应用程序清单文件。 替换*ManifestFileName*清单文件和扩展的名称。 替换*证书*的证书文件并替换为相对或完全限定路径*密码*替换为证书的密码。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令以登录为外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单。 Visual Studio 创建的临时证书不建议以部署到生产环境中。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 键入以下命令以更新并对签名部署清单文件，替换占位符名称，如在上一步中所示。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令以更新和 Excel 外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序部署清单进行签名。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. （可选） 将复制的主部署清单 (*发布\\\<appname >.application*) 到你的版本部署目录 (*publish\Application 文件\\\<appname > _\<版本 >*)。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>更新和应用程序和部署清单重新签名
 此过程假定您已对你的应用程序清单文件中做出了更改 (*.manifest*)，但有一些其他已更新的文件。 当文件更新时，也必须更新表示的文件的哈希。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 更新和重新签名的应用程序和部署清单

1. 打开**Visual Studio 命令提示符**窗口。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 删除 *.deploy*文件扩展名从发布中的文件输出文件夹。

4. 键入以下命令以使用更新后的文件的新哈希更新应用程序清单和应用程序清单文件进行签名。 替换*ManifestFileName*清单文件和扩展的名称。 替换*证书*的证书文件并替换为相对或完全限定路径*密码*替换为证书的密码。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令以登录为外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单。 Visual Studio 创建的临时证书不建议以部署到生产环境中。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 键入以下命令以更新并对签名部署清单文件，替换占位符名称，如在上一步中所示。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，可以运行以下命令以更新和 Excel 外接程序、 Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序部署清单进行签名。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. 添加 *.deploy*到文件，文件扩展名，但应用程序和部署清单文件。

7. （可选） 将复制的主部署清单 (*发布\\\<appname >.application*) 到你的版本部署目录 (*publish\Application 文件\\\<appname > _\<版本 >*)。

## <a name="see-also"></a>请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：设置 ClickOnce 应用程序安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：调试具有受限权限的 ClickOnce 应用程序](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [如何：将受信任的发布服务器添加到 ClickOnce 应用程序的客户端计算机](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)