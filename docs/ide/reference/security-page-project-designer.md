---
title: ”项目设计器“ ->“安全”页
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesSecurity
- vb.XBAPProjectPropertiesSecurity
helpviewer_keywords:
- Project Designer, Security page
- Security page in Project Designer
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f11b14dd116ea95bda2cc7fad7ac8df634435c9
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926098"
---
# <a name="security-page-project-designer"></a>”项目设计器“ ->“安全”页

“项目设计器”的“安全”页用于配置使用 ClickOnce 部署部署的应用程序的代码访问安全性设置   。 有关详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../../deployment/code-access-security-for-clickonce-applications.md)。

要访问“安全”页，请在“解决方案资源管理器”中单击一个项目节点，然后在“项目”菜单单击“属性”     。 显示“项目设计器”时，单击“安全性”选项卡   。

## <a name="security-settings"></a>安全设置

 **“启用 ClickOnce 安全设置”**

确定是否在设计时启用安全设置。 清除此选项后，“安全”页上的所有其他选项均不可用  。

> [!NOTE]
> 使用“发布”向导发布应用程序时，会自动启用此选项  。

选择此选项时，可以选择以下两个单选按钮之一：“这是完全信任应用程序”或“这是部分信任应用程序”   。

对于 WPF Web 浏览器应用程序项目，默认选择此选项。

对于所有其他项目类型，默认清除此选项。

 **这是完全信任的应用程序**

如果选择此选项，在客户端计算机上安装或运行应用程序时，此应用程序会请求完全信任权限。 如果可能，请避免使用完全信任，因为这会授予应用程序对文件系统和注册表等资源的无限制访问权限。

对于 WPF Web 浏览器应用程序项目，此选项默认设置为“部分信任”。

对于所有其他项目类型，此选项默认设置为“完全信任”。

 **这是部分信任应用程序**

如果选择此选项，在客户端计算机上安装或运行应用程序时，此应用程序会请求部分信任权限。 “部分信任”表示仅运行在请求的代码访问安全权限下允许的操作  。 有关如何配置安全权限的详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../../deployment/code-access-security-for-clickonce-applications.md)。

通过配置“ClickOnce 安全权限”区域中的选项，可以指定部分信任安全设置  。

## <a name="clickonce-security-permissions"></a>ClickOnce 安全权限

 **将要从中安装应用程序的区域**

指定一组默认的代码访问安全权限。 对于受限的权限设置，选择“Internet”或“本地 Intranet”，或者选择“(自定义)”配置自定义权限集    。 如果应用程序请求的权限比区域中授予的多，则会出现 ClickOnce 信任提示，要求最终用户授予其他权限。 有关如何配置安全权限的详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../../deployment/code-access-security-for-clickonce-applications.md)。

对于 WPF Web 浏览器应用程序项目，此选项默认设置为“Internet”  。

 **编辑权限 XML**

打开应用程序清单模板 (app.manifest)，配置“(自定义)”权限集的权限  。

 **高级**

打开[“高级安全设置”对话框](../../ide/reference/advanced-security-settings-dialog-box.md)，该对话框用于为调试应用程序的设置配置受限权限。 在调试过程中会检查这些设置，权限异常表示应用程序需要的权限可能超过了区域中定义的权限。

## <a name="see-also"></a>另请参阅

- <xref:System.Security.Permissions.WebBrowserPermission>
- <xref:System.Security.Permissions.MediaPermission>
- [ClickOnce 应用程序的代码访问安全性](../../deployment/code-access-security-for-clickonce-applications.md)
- [如何：启用 ClickOnce 安全设置](../../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：设置 ClickOnce 应用程序的安全区域](../../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：设置 ClickOnce 应用程序的自定义权限](../../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限调试 ClickOnce 应用程序](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [ClickOnce 安全和部署](../../deployment/clickonce-security-and-deployment.md)
- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [“高级安全设置”对话框](../../ide/reference/advanced-security-settings-dialog-box.md)