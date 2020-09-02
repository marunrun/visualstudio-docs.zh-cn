---
title: ClickOnce 和应用程序设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, application settings
ms.assetid: 891caba6-faef-4a3c-8f71-60e6fadb60eb
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8e1ffe6d6f32cfad137d5890715a5a0032a29d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696691"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

利用 Windows 窗体的应用程序设置，可以轻松地在客户端上创建、存储和维护自定义应用程序和用户首选项。 下面的文档介绍应用程序设置文件在 ClickOnce 应用程序中的工作方式，以及 ClickOnce 如何在用户升级到下一个版本时迁移设置。  
  
 以下信息仅适用于默认应用程序设置提供程序（ <xref:System.Configuration.LocalFileSettingsProvider> 类）。 如果提供自定义提供程序，则该提供程序将确定它如何存储其数据，以及如何在不同版本之间升级其设置。 有关应用程序设置提供程序的详细信息，请参阅 [应用程序设置体系结构](https://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562)。  
  
## <a name="application-settings-files"></a>应用程序设置文件  
 应用程序设置使用两个文件： *app*.exe.config 和 user.config，其中 *app* 是 Windows 窗体应用程序的名称。 当应用程序首次存储用户范围的设置时，将在客户端上创建 user.config。 相反，*应用*.exe.config 会在部署之前存在，前提是你为设置定义了默认值。 使用 " **发布** " 命令时，Visual Studio 将自动包含此文件。 如果使用 Mage.exe 或 MageUI.exe 创建 ClickOnce 应用程序，则在填充应用程序清单时，必须确保将此文件包含在应用程序的其他文件中。  
  
 在不使用 ClickOnce 部署的 Windows 窗体应用程序中，应用程序的 *应用*.exe.config 文件存储在应用程序目录中，而 user.config 文件存储在用户的 " **文档和设置** " 文件夹中。 在 ClickOnce 应用程序中， *应用*.exe.config 位于 clickonce 应用程序缓存内的应用程序目录中，并 user.config 驻留在该应用程序的 clickonce 数据目录中。  
  
 无论你部署应用程序的方式如何，应用程序设置都可以确保对 *应用* 程序.exe.config 安全读取访问权限，并确保对 user.config 的安全读/写访问。  
  
 在 ClickOnce 应用程序中，应用程序设置所使用的配置文件的大小受 ClickOnce 缓存大小的限制。 有关详细信息，请参阅 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。  
  
## <a name="version-upgrades"></a>版本升级  
 就像 ClickOnce 应用程序的每个版本都与所有其他版本隔离时，ClickOnce 应用程序的应用程序设置也会独立于其他版本的设置。 当你的用户升级到应用程序的更高版本时，应用程序设置会将最近 (的最高编号) 版本的设置与更新版本提供的设置进行比较，并将设置合并到一组新的设置文件中。  
  
 下表描述了应用程序设置如何决定要复制哪些设置。  
  
|更改类型|升级操作|  
|--------------------|--------------------|  
|设置已添加到 *应用*.exe.config|新设置将合并到当前版本的 *应用* 中.exe.config|  
|已从 *应用*.exe.config 中删除设置|旧设置将从当前版本的 *应用* 中删除.exe.config|  
|设置的默认值已更改;本地设置仍设置为 user.config 中的原始默认值|设置将合并到当前版本的 user.config 中，新默认值为|  
|设置的默认值已更改;设置在 user.config 中设置为非默认值|设置将合并到当前版本的 user.config 中，并保留非默认值|  
  
 如果已创建自己的应用程序设置包装器类，并且想要自定义更新逻辑，则可以重写 <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> 方法。  
  
## <a name="clickonce-and-roaming-settings"></a>ClickOnce 和漫游设置  
 ClickOnce 不适用于漫游设置，这允许你的设置文件在网络上的计算机之间执行操作。 如果需要漫游设置，你将需要实现通过网络存储设置的应用程序设置提供程序，或者开发你自己的自定义设置类，以便在远程计算机上存储设置。 有关设置提供程序的详细信息，请参阅 [应用程序设置体系结构](https://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562)。  
  
## <a name="see-also"></a>另请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [应用程序设置概述](https://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc)   
 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)   
 [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
