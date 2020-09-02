---
title: 如何对应用程序和部署清单进行重新签名 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 1905ea32a9899a1262e146f264e0a1179f0e8c6e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85382193"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>如何：为应用程序和部署清单重新签名
对 Windows 窗体应用程序的应用程序清单中的部署属性进行更改后，Windows Presentation Foundation 应用程序 (xbap) 或 Office 解决方案，则必须使用证书对应用程序清单和部署清单进行重新签名。 此过程有助于确保不会在最终用户计算机上安装经过篡改的文件。

 如果你的客户想要将应用程序和部署清单签名为自己的证书，则可以对清单进行重新签名的另一种情况。

## <a name="re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单重新签名
 此过程假定您已对应用程序清单 *文件 () * 进行了更改。 有关详细信息，请参阅 [如何：更改部署属性](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472)。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>用 Mage.exe 对应用程序清单和部署清单进行重新签名

1. 打开 **Visual Studio 命令提示符** 窗口。

2. 将目录更改为包含要签署的清单文件的文件夹。

3. 键入以下命令，对应用程序清单文件进行签名。 将 *ManifestFileName* 替换为清单文件的名称和扩展名。 将 *证书* 替换为证书文件的相对或完全限定路径，并将 *password* 替换为证书的密码。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，你可以运行以下命令，为外接程序、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单签名。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 键入以下命令以更新部署清单文件并对其进行签名，如前一步骤所示替换占位符名称。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，你可以运行以下命令，为 Excel 外接程序、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序更新和签名部署清单。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. （可选）将主部署清单 (*publish \\ \<appname> *) 复制到版本部署目录 (*publish\Application Files \\ \<appname> _ \<version> *) 。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>更新和重新签名应用程序和部署清单
 此过程假定你已对应用程序清单 *文件 () * 进行了更改，但有其他已更新的文件。 更新文件后，还必须更新表示该文件的哈希。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>更新应用程序和部署清单并将其重新签名 Mage.exe

1. 打开 **Visual Studio 命令提示符** 窗口。

2. 将目录更改为包含要签署的清单文件的文件夹。

3. 从 "发布输出" 文件夹的文件中删除 *.deploy* 文件扩展名。

4. 键入以下命令，将应用程序清单更新为更新的文件的新哈希，并对应用程序清单文件进行签名。 将 *ManifestFileName* 替换为清单文件的名称和扩展名。 将 *证书* 替换为证书文件的相对或完全限定路径，并将 *password* 替换为证书的密码。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，你可以运行以下命令，为外接程序、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序的应用程序清单签名。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 键入以下命令以更新部署清单文件并对其进行签名，如前一步骤所示替换占位符名称。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，你可以运行以下命令，为 Excel 外接程序、Windows 窗体应用程序或 Windows Presentation Foundation 浏览器应用程序更新和签名部署清单。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. 将 *.deploy* 文件扩展名添加回文件（应用程序和部署清单文件除外）。

7. （可选）将主部署清单 (*publish \\ \<appname> *) 复制到版本部署目录 (*publish\Application Files \\ \<appname> _ \<version> *) 。

## <a name="see-also"></a>请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：为 ClickOnce 应用程序设置自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)
- [如何：为 ClickOnce 应用程序向客户端计算机添加受信任的发布者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)