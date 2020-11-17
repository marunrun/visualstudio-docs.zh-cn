---
title: 使用 ClickOnce 部署 .NET Windows 桌面应用程序
ms.date: 10/15/2020
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder, ClickOnce
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: john-hart
ms.author: JohnHart
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: f2d7b500caacf320df599843e45cc4e93b4f3e69
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94447152"
---
# <a name="deploy-a-net-windows-desktop-application-using-clickonce"></a>使用 ClickOnce 部署 .NET Windows 桌面应用程序

从 Visual Studio 2019 版本 16.8 开始，可以从 Visual Studio 使用“发布”工具，通过 ClickOnce 发布 .NET Core 3.1 或更高版本的 Windows 桌面应用程序。

> [!NOTE]
> 如果需要发布 .NET Framework Windows 应用程序，请参阅[使用 ClickOnce 部署桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)（C# 或 Visual Basic）。

## <a name="publishing-with-clickonce"></a>使用 ClickOnce 进行发布

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）  。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-clickonce-solution-explorer.png "选择发布")

1. 如果先前配置了任何发布配置文件，则“发布”页会显示。 选择“新建”。

1. 在“发布”向导中，选择“文件夹”。

    ![选择文件夹作为发布目标](../deployment/media/quickstart-clickonce-publish-folder-category.png "选择文件夹")

1. 在“特定目标”页上，选择“ClickOnce” 。

    ![选择 ClickOnce 作为特定目标](../deployment/media/quickstart-clickonce-publish-folder-target.png "选择 ClickOnce")

1. 输入路径或选择“浏览”以选择发布位置。

    ![指定发布位置的路径](../deployment/media/quickstart-clickonce-publish-location.png "输入路径")

1. 在“安装位置”页中，选择用户安装应用程序的位置。

    ![指定文件夹的路径](../deployment/media/quickstart-clickonce-install-location.png "选择安装位置")

1. 在“设置”页中，可以提供 ClickOnce 所需的设置。

1. 如果选择从 UNC 路径或网站安装，则可以通过此页指定应用程序是否可脱机使用。 选中时，此选项会在用户“开始”菜单上列出应用程序，并允许在发布新版本时自动更新应用程序。 默认情况下，可以从安装位置获取更新。  如果希望将另一个位置用于更新，则可以使用“更新设置”链接指定该位置。 如果不希望应用程序可脱机使用，则它会从安装位置运行。

    ![指定发布设置](../deployment/media/quickstart-clickonce-unc-settings.png "选择发布设置")

1. 如果选择从 CD、DVD 或 USB 盘进行安装，则还可以通过此页指定应用程序是否支持自动更新。 如果选择支持更新，则“更新位置”是必填项，并且必须是有效的 UNC 路径或网站。

    ![选择发布设置](../deployment/media/quickstart-clickonce-settings.png "选择发布设置")

在此页中能够通过页面顶部的链接指定要包含在安装程序中的“应用程序文件”、要安装的“必备组件”包以及其他“选项”  。

此外，还可以在此页中设置发布版本，以及版本是否会随着每次发布而自动递增。

> [!NOTE]
> 发布版本号对于每个 ClickOnce 配置文件都是唯一的。 如果计划使用多个配置文件，则需要记住这一点。

10. 在“签名清单”页上，可以指定是否应对清单进行签名以及要使用的证书。

    ![为 ClickOnce 清单签名](../deployment/media/quickstart-clickonce-sign-manifests.png)

1. 在“配置”页上，可以选择所需的项目配置。

     ![指定发布配置](../deployment/media/quickstart-clickonce-configuration.png)

    有关要选择的设置的其他帮助，请参阅以下内容：

    - [依赖于框架的部署与自包含部署](/dotnet/core/deploying/)
    - [目标运行时标识符（可移植 RID 等）](/dotnet/core/rid-catalog)
    - [调试和发布配置](../ide/understanding-build-configurations.md)

1. 选择“完成”以保存新 ClickOnce 发布配置文件。

1. 在“摘要”页上，选择“发布”，Visual Studio 会生成项目并将其发布到指定发布文件夹 。 此页还显示配置文件摘要。

    ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-clickonce-summary.png)

1. 若要重新发布，请选择“发布”。

## <a name="next-steps"></a>后续步骤

对于 .NET 应用：

- [部署 .NET Framework 和应用程序](/dotnet/framework/deployment/)
- [ClickOnce 参考](clickonce-reference.md)
