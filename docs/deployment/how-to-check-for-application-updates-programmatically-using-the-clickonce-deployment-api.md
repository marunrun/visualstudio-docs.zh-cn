---
title: 使用 ClickOnce 部署 API 的自动应用更新
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
ms.openlocfilehash: 9f47c82311f26c5ca469f03783b785545bda2182
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260824"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>如何：使用 ClickOnce 部署 API 以编程方式检查是否有应用程序更新
ClickOnce 提供两种方法在部署之后更新的应用程序。 在第一种方法，可以配置 ClickOnce 部署自动检查更新在一定时间间隔。 在第二个方法中，可以编写使用的代码<xref:System.Deployment.Application.ApplicationDeployment>类，以检查更新的基于事件，如用户请求。

 以下过程显示执行以编程方式更新一些代码，还介绍了如何配置 ClickOnce 部署，以便以编程方式更新检查。

 若要以编程方式更新 ClickOnce 应用程序，必须指定更新的位置。 这有时称为部署提供程序。 有关设置此属性的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

> [!NOTE]
> 此外可以使用如下所述来部署你的应用程序从一个位置，但从另一个更新的技术。 有关详细信息，请参阅[如何：指定部署更新的替换位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)。

### <a name="to-check-for-updates-programmatically"></a>若要以编程方式检查更新

1. 创建新的 Windows 窗体应用程序使用您首选的命令行或 visual 工具。

2. 创建任何按钮、 菜单项或其他用户界面项你希望用户能够进行选择以检查更新。 从该项目的事件处理程序，调用以下方法，以检查并安装更新。

     [!code-csharp[ClickOnceAPI#6](../deployment/codesnippet/CSharp/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cs)]
     [!code-cpp[ClickOnceAPI#6](../deployment/codesnippet/CPP/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.cpp)]
     [!code-vb[ClickOnceAPI#6](../deployment/codesnippet/VisualBasic/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api_1.vb)]

3. 编译应用程序。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 Mage.exe 部署以编程方式检查更新的应用程序

- 按照说明部署你的应用程序中所述使用 Mage.exe[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 在调用 Mage.exe 生成部署清单，请确保使用命令行开关`providerUrl`，并指定 ClickOnce 检查更新的位置的 URL。 如果你的应用程序将更新从[ http://www.adatum.com/MyApp ](http://www.adatum.com/MyApp)，例如，若要生成的部署清单的调用可能如下所示：

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 MageUI.exe 部署以编程方式检查更新的应用程序

- 按照说明部署你的应用程序中所述使用 Mage.exe[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 上**部署选项**选项卡上，设置**开始位置**字段检查更新的 ClickOnce 应用程序清单。 上**更新选项**选项卡上，清除**此应用程序应检查更新**复选框。

## <a name="net-framework-security"></a>.NET Framework 安全性
 你的应用程序必须具有完全信任权限，用于以编程方式更新。

## <a name="see-also"></a>请参阅
- [如何：指定部署更新的其他位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)