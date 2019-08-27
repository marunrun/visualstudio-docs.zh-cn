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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696691"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce 和应用程序设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows 窗体的应用程序设置，可以轻松地创建、 存储和维护自定义应用程序和客户端上的用户首选项。 以下文档介绍了在 ClickOnce 应用程序中，应用程序设置文件的工作方式和用户升级到下一版本时，ClickOnce 如何迁移设置。  
  
 下面的信息仅适用于默认应用程序设置提供程序，<xref:System.Configuration.LocalFileSettingsProvider>类。 如果提供自定义提供程序，它将其数据的存储和如何升级其版本之间的设置将确定该提供程序。 应用程序设置提供程序的详细信息，请参阅[应用程序设置体系结构](https://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562)。  
  
## <a name="application-settings-files"></a>应用程序设置文件  
 应用程序设置使用两个文件：*应用程序*.exe.config 并且 user.config，其中*应用*是 Windows 窗体应用程序的名称。 user.config 创建你的应用程序存储用户范围设置的客户端第一个时间。 *应用*.exe.config 中，与此相反，将在部署之前如果存在定义设置的默认值。 Visual Studio 将在使用时自动包括此文件及其**发布**命令。 创建 ClickOnce 应用程序使用 Mage.exe 或 MageUI.exe 中，你必须确保此文件是否包含与填充应用程序清单时，你的应用程序的其他文件。  
  
 在 Windows 窗体应用程序中不使用 ClickOnce，应用程序部署*应用程序*.exe.config 文件存储在应用程序目录中，而 user.config 文件存储在用户的**文档和设置**文件夹。 在 ClickOnce 应用程序中，*应用*。 exe.config 居住在 ClickOnce 应用程序缓存中，应用程序目录，在该应用程序的 ClickOnce 数据目录中的 user.config 存在。  
  
 无论你部署应用程序的方式，应用程序设置可确保安全的读取访问权限*应用*.exe.config，并且保存到 user.config 安全的读/写访问。  
  
 在 ClickOnce 应用程序，使用应用程序设置的配置文件的大小受 ClickOnce 缓存的大小。 有关详细信息，请参阅[ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。  
  
## <a name="version-upgrades"></a>版本升级  
 就像每个版本的 ClickOnce 应用程序是独立于所有其他版本，ClickOnce 应用程序的应用程序设置彼此之间以及其他版本的设置。 在你的用户升级到更高版本的应用程序，应用程序设置将针对提供的更新的版本和合并到一组新的设置文件的设置的设置设置的最新 （最高编号） 版本设置进行比较。  
  
 下表描述了应用程序设置如何决定要复制的设置。  
  
|更改类型|升级操作|  
|--------------------|--------------------|  
|设置添加到*应用*。 exe.config|新的设置合并到当前版本*应用*。 exe.config|  
|删除从设置*应用*。 exe.config|从当前版本中删除旧的设置*应用*。 exe.config|  
|设置的默认更改;本地设置仍设置为原始默认值在 user.config|设置的值被合并到新的默认值的当前版本 user.config|  
|设置的默认更改;设置设置为非默认值在 user.config|设置保留为非默认值已合并到当前版本 user.config|  
  
 如果您已创建你自己的应用程序设置包装类，并想要自定义更新逻辑，则可以重写<xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A>方法。  
  
## <a name="clickonce-and-roaming-settings"></a>ClickOnce 和漫游设置  
 ClickOnce 并不适用于漫游设置，它允许您以跟随你跨计算机在网络上的设置文件。 如果您需要漫游设置，将需要以实现将设置存储在网络上的应用程序设置提供程序或开发自己的自定义设置类来存储在远程计算机上的设置。 在设置提供程序的详细信息，请参阅[应用程序设置体系结构](https://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562)。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [应用程序设置概述](https://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc)   
 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)   
 [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
