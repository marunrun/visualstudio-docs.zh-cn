---
title: Devenv 命令行开关，适用于 VSPackage 开发 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- /setup command line switch
- /resetskippkgs command line switch
- /noVSIP command line switch
- /rootsuffix command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97ce429a7140d7b95393c2dcb8b34491b3adfefa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185283"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 开发的 Devenv 命令行开关
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 允许开发人员在执行 devenv.exe 时从命令行自动执行任务， (IDE) 启动 Visual Studio 集成开发环境。  
  
 任务包括：  
  
- 从 IDE 外部部署预先设计的配置中的应用程序。  
  
- 使用预设生成设置或调试配置自动生成项目。  
  
- 将 IDE 加载到 IDE 外部的特定配置。 此外，您可以在启动时自定义 IDE。  
  
## <a name="guidelines-for-switches"></a>开关指南  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 文档介绍用户级 devenv 命令行开关。 有关详细信息，请参阅 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)。 Devenv 还支持其他可用于 VSPackage 开发、部署和调试的命令行开关。  
  
|命令行开关|说明|  
|--------------------------|-----------------|  
|/safemode|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在安全模式下启动，只加载默认 IDE 和服务。 /Safemode 开关可防止在启动时加载所有第三方 Vspackage [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，从而确保稳定的执行。<br /><br /> 此开关不带参数。|  
|/resetskippkgs|清除所有要避免加载有问题的 Vspackage 的用户添加的 "跳过加载" 选项，然后启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 如果存在 SkipLoading 标记，则会禁用 VSPackage 的加载。 清除标记会重新启用 VSPackage 的加载。<br /><br /> 此开关不带参数。|  
|/rootsuffix|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]使用备用位置启动。 以下命令由安装程序创建的快捷方式运行 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] ：<br /><br /> devenv/RootSuffix exp<br /><br /> 在这种情况下，exp 会标识具有特定后缀的位置，例如 10.0 Exp 而不是10.0。 利用实验实例，您可以从用于编写代码的实例中单独调试 VSPackage [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。<br /><br /> 此开关可以采用标识您使用 VSRegEx.exe 创建的位置的任何字符串。 有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。|  
|/splash|照常显示 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 初始屏幕，然后在显示主 IDE 之前显示消息框。 使用消息框，您可以研究初始屏幕，以检查 VSPackage 的产品图标，例如。<br /><br /> 此开关不带参数。|  
  
## <a name="see-also"></a>另请参阅  
 [添加命令行开关](../extensibility/adding-command-line-switches.md)   
 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
