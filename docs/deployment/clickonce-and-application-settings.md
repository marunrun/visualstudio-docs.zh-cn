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
ms.openlocfilehash: 153df515fc762b7262dce81d8c1d1c4fe617ad61
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900606"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
Windows 窗体的应用程序设置，可以轻松地创建、 存储和维护自定义应用程序和客户端上的用户首选项。 以下文档介绍了在 ClickOnce 应用程序中，应用程序设置文件的工作方式和用户升级到下一版本时，ClickOnce 如何迁移设置。

 下面的信息仅适用于默认应用程序设置提供程序， \<xref:System.Configuration.LocalFileSettingsProvider > 类。 如果提供自定义提供程序，它将其数据的存储和如何升级其版本之间的设置将确定该提供程序。 应用程序设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="application-settings-files"></a>应用程序设置文件
 应用程序设置使用两个文件： *\<应用程序 >。 exe.config*并*user.config*，其中*应用*是 Windows 窗体应用程序的名称。 *user.config*创建你的应用程序存储用户范围设置的客户端第一个时间。 *\<应用程序 >。 exe.config*，与此相反，将在部署之前如果存在定义设置的默认值。 Visual Studio 将在使用时自动包括此文件及其**发布**命令。 如果在 ClickOnce 应用程序使用创建*Mage.exe*或*MageUI.exe*，您必须确保此文件是包含在你的应用程序的其他文件时填充应用程序清单。

 在 Windows 窗体应用程序中不使用 ClickOnce，应用程序部署 *\<应用程序 >。 exe.config*文件存储在应用程序目录中，而*user.config*文件存储在用户的**文档和设置**文件夹。 在 ClickOnce 应用程序中， *\<应用程序 >。 exe.config*驻留在 ClickOnce 应用程序缓存中，在应用程序目录中并*user.config*居住在 ClickOnce 数据目录为该应用程序。

 无论你部署应用程序的方式，应用程序设置可确保安全的读取访问权限 *\<应用程序 >。 exe.config*，和安全的读/写访问权限*user.config*。

 在 ClickOnce 应用程序，使用应用程序设置的配置文件的大小受 ClickOnce 缓存的大小。 有关详细信息，请参阅[ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="version-upgrades"></a>版本升级
 就像每个版本的 ClickOnce 应用程序是独立于所有其他版本，ClickOnce 应用程序的应用程序设置彼此之间以及其他版本的设置。 在你的用户升级到更高版本的应用程序，应用程序设置将针对提供的更新的版本和合并到一组新的设置文件的设置的设置设置的最新 （最高编号） 版本设置进行比较。

 下表描述了应用程序设置如何决定要复制的设置。

|更改类型|升级操作|
|--------------------|--------------------|
|设置添加到 *\<应用程序 >。 exe.config*|新的设置合并到当前版本 *\<应用程序 >。 exe.config*|
|删除从设置 *\<应用程序 >。 exe.config*|从当前版本中删除旧的设置 *\<应用程序 >。 exe.config*|
|设置的默认更改;本地设置仍设置为原始默认值在*user.config*|设置合并到当前版本*user.config*与作为值的新默认值|
|设置的默认更改;将组设置为在非默认*user.config*|设置合并到当前版本*user.config*与保留的非默认值|

如果您已创建你自己的应用程序设置包装类，并想要自定义更新逻辑，则可以重写\<xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A > 方法。

## <a name="clickonce-and-roaming-settings"></a>ClickOnce 和漫游设置
 ClickOnce 并不适用于漫游设置，它允许您以跟随你跨计算机在网络上的设置文件。 如果您需要漫游设置，将需要以实现将设置存储在网络上的应用程序设置提供程序或开发自己的自定义设置类来存储在远程计算机上的设置。 在设置提供程序的详细信息，请参阅[应用程序设置体系结构](/dotnet/framework/winforms/advanced/application-settings-architecture)。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [应用程序设置概述](/dotnet/framework/winforms/advanced/application-settings-overview)
- [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)