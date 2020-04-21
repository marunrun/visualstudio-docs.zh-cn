---
title: 如何：重新签名应用程序和部署清单 |微软文档
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
ms.openlocfilehash: fc69ce1f79644d7f4b35fbb1c1e3a41691761390
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649191"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>如何：为应用程序和部署清单重新签名
更改 Windows 窗体应用程序、Windows 演示文稿基础应用程序 （xbap） 或 Office 解决方案的应用程序清单中的部署属性后，必须使用证书重新签名应用程序和部署清单。 此过程有助于确保不会在最终用户计算机上安装经过篡改的文件。

 另一种可能重新签名清单的情况是，您的客户希望使用自己的证书对应用程序和部署清单进行签名。

## <a name="re-sign-the-application-and-deployment-manifests"></a>对应用程序清单和部署清单重新签名
 此过程假定您已经对应用程序清单文件 *（.manifest）* 进行了更改。 有关详细信息，请参阅[如何：更改部署属性](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472)。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 重新签名应用程序和部署清单

1. 打开**可视化工作室命令提示窗口**。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 键入以下命令对应用程序清单文件进行签名。 将*清单文件名称*替换为清单文件的名称以及扩展名。 将*证书*替换为证书文件的相对或完全限定路径，并将*密码*替换为证书的密码。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，您可以运行以下命令来为外接程序、Windows 窗体应用程序或 Windows 演示文稿基础浏览器应用程序签名应用程序清单。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 键入以下命令以更新和签名部署清单文件，替换占位符名称，如上一步骤中所述。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，您可以运行以下命令来更新和签署 Excel 外接程序、Windows 窗体应用程序或 Windows 演示文稿基础浏览器应用程序的部署清单。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 或者，将主部署清单（*发布\\\<应用程序名称>.应用程序*）复制到版本部署目录（*发布\应用程序文件\\\<应用程序名称>_\<版本>*）。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>更新并重新签署应用程序和部署清单
 此过程假定您已经对应用程序清单文件 *（.manifest）* 进行了更改，但还有其他文件已更新。 更新文件时，还必须更新表示文件的哈希值。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>使用 Mage.exe 更新和重新签署应用程序和部署清单

1. 打开**可视化工作室命令提示窗口**。

2. 将目录更改为包含要签名的清单文件的文件夹。

3. 从发布输出文件夹中的文件中删除 *.deploy*文件扩展名。

4. 键入以下命令以使用更新文件的新哈希更新应用程序清单，并签署应用程序清单文件。 将*清单文件名称*替换为清单文件的名称以及扩展名。 将*证书*替换为证书文件的相对或完全限定路径，并将*密码*替换为证书的密码。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     例如，您可以运行以下命令来为外接程序、Windows 窗体应用程序或 Windows 演示文稿基础浏览器应用程序签名应用程序清单。 不建议将 Visual Studio 创建的临时证书部署到生产环境中。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 键入以下命令以更新和签名部署清单文件，替换占位符名称，如上一步骤中所述。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     例如，您可以运行以下命令来更新和签署 Excel 外接程序、Windows 窗体应用程序或 Windows 演示文稿基础浏览器应用程序的部署清单。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. 将 *.deploy*文件扩展名添加回文件，应用程序和部署清单文件除外。

7. 或者，将主部署清单（*发布\\\<应用程序名称>.应用程序*）复制到版本部署目录（*发布\应用程序文件\\\<应用程序名称>_\<版本>*）。

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：为 ClickOnce 应用程序设置自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)
- [如何：将受信任的发布者添加到用于 ClickOnce 应用程序的客户端计算机](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：配置点击一次信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)