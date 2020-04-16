---
title: 使用 ClickOnce 部署 API 自动应用更新
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9300fbf8b348b1016d36d414d17a66c45f6494b9
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444612"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>如何：使用 ClickOnce 部署 API 以编程方式检查应用程序更新
ClickOnce 提供了两种在部署应用程序后更新应用程序的方法。 在第一种方法中，您可以配置 ClickOnce 部署，以便在特定间隔内自动检查更新。 在第二种方法中，可以编写使用<xref:System.Deployment.Application.ApplicationDeployment>类根据事件（如用户请求）检查更新的代码。

 以下过程显示了一些用于执行编程更新的代码，并介绍了如何配置 ClickOnce 部署以启用编程更新检查。

 为了以编程方式更新 ClickOnce 应用程序，必须指定更新的位置。 这有时称为部署提供程序。 有关设置此属性的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

> [!NOTE]
> 您还可以使用下面描述的技术从一个位置部署应用程序，但从另一个位置更新应用程序。 有关详细信息，请参阅[如何：为部署更新指定备用位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 使用首选的命令行或可视工具创建新的 Windows 窗体应用程序。

2. 创建您希望用户选择以检查更新的任何按钮、菜单项或其他用户界面项。 从该项目的事件处理程序中，调用以下方法来检查并安装更新。

     [!code-csharp[ClickOnceAPI#6](../deployment/codesnippet/CSharp/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cs)]
     [!code-cpp[ClickOnceAPI#6](../deployment/codesnippet/CPP/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cpp)]
     [!code-vb[ClickOnceAPI#6](../deployment/codesnippet/VisualBasic/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.vb)]

3. 编译应用程序。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 Mage.exe 部署以编程方式检查更新的应用程序

- 按照在演练中解释的使用 Mage.exe 部署应用程序的说明[：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 调用 Mage.exe 生成部署清单时，请确保使用命令行开关`providerUrl`，并指定 ClickOnce 应检查更新的 URL。 例如，如果应用程序将从`http://www.adatum.com/MyApp`中更新，则生成部署清单的调用可能如下所示：

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 MageUI.exe 部署以编程方式检查更新的应用程序

- 按照在演练中解释的使用 Mage.exe 部署应用程序的说明[：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 在 **"部署选项"** 选项卡上，将 **"开始位置"** 字段设置为应用程序清单 ClickOnce 应检查更新。 在"**更新选项**"选项卡上，清除**此应用程序应选中更新**复选框。

## <a name="net-framework-security"></a>.NET Framework 安全性
 您的应用程序必须具有完全信任的权限才能使用编程更新。

## <a name="see-also"></a>请参阅
- [如何：为部署更新指定备用位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)