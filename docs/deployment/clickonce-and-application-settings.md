---
title: ClickOnce 和应用程序设置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, application settings
ms.assetid: 891caba6-faef-4a3c-8f71-60e6fadb60eb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a72b5bc3f3645d9af1008f2c178ab285e8b45449
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184128"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
利用 Windows 窗体的应用程序设置，可以轻松地在客户端上创建、存储和维护自定义应用程序和用户首选项。 下面的文档介绍应用程序设置文件在 ClickOnce 应用程序中的工作方式，以及 ClickOnce 如何在用户升级到下一个版本时迁移设置。

 以下信息仅适用于默认应用程序设置提供程序（ <xref:System.Configuration.LocalFileSettingsProvider> 类）。 如果提供自定义提供程序，则该提供程序将确定它如何存储其数据，以及如何在不同版本之间升级其设置。 有关应用程序设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="application-settings-files"></a>应用程序设置文件
 应用程序设置使用两个文件： * \<app> .exe .config*和*用户 .config*，其中*app*是 Windows 窗体应用程序的名称。 当应用程序首次存储用户范围的设置时，将在客户端上创建*用户。* 相反，如果您为设置定义了默认值，则在部署之前将存在* \<app> .exe .config*。 使用 "**发布**" 命令时，Visual Studio 将自动包含此文件。 如果使用*mage.exe*或*mageui.exe*创建 ClickOnce 应用程序，则在填充应用程序清单时，必须确保将此文件包含在应用程序的其他文件中。

 在不使用 ClickOnce 部署的 Windows 窗体应用程序中，应用程序的* \<app> .exe*文件存储在应用程序目录中，而用户的 *.config*文件存储在用户的 "**文档和设置**" 文件夹中。 在 ClickOnce 应用程序中，位于 ClickOnce 应用程序缓存内的应用程序目录中，而*用户 .config*位于该应用程序的 clickonce 数据目录* \<app> 中。*

 无论部署应用程序的方式如何，应用程序设置都可确保对* \<app> app.config*的安全读取访问权限以及对*用户的*安全读/写访问权限。

 在 ClickOnce 应用程序中，应用程序设置所使用的配置文件的大小受 ClickOnce 缓存大小的限制。 有关详细信息，请参阅[ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="version-upgrades"></a>版本升级
 就像 ClickOnce 应用程序的每个版本都与所有其他版本隔离时，ClickOnce 应用程序的应用程序设置也会独立于其他版本的设置。 当你的用户升级到应用程序的更高版本时，应用程序设置会根据更新版本提供的设置来比较最新（编号最高）版本的设置，并将设置合并到一组新的设置文件中。

 下表描述了应用程序设置如何决定要复制哪些设置。

|更改类型|升级操作|
|--------------------|--------------------|
|设置已添加到* \<app> .exe*|新设置将合并到当前版本的* \<app> .exe. .config*|
|从* \<app> .exe*中删除的设置|旧的设置已从当前版本的* \<app> .exe. .config*|
|设置的默认值已更改;在*用户 .config*中，本地设置仍设置为原始默认值|设置将合并到当前版本的*用户 .config*中，新的默认值为|
|设置的默认值已更改;设置在*用户 .config*中设置为非默认值|此设置将合并到当前版本的*用户 .config*中，并保留非默认值|

如果已创建自己的应用程序设置包装器类，并且想要自定义更新逻辑，则可以重写 <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> 方法。

## <a name="clickonce-and-roaming-settings"></a>ClickOnce 和漫游设置
 ClickOnce 不适用于漫游设置，这允许你的设置文件在网络上的计算机之间执行操作。 如果需要漫游设置，你将需要实现通过网络存储设置的应用程序设置提供程序，或者开发你自己的自定义设置类，以便在远程计算机上存储设置。 有关设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [应用程序设置概述](/dotnet/framework/winforms/advanced/application-settings-overview)
- [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)