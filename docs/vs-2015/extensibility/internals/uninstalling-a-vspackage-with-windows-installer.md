---
title: 卸载具有 Windows Installer 的 VSPackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9a309779850dd33b77b426beb5627f61c40c2c4f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675231"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在大多数情况下，Windows Installer 只需通过 "撤消" 安装 VSPackage 的操作即可卸载你的 VSPackage。 还必须在卸载后运行的 [命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md) 中讨论的自定义操作。 由于对 devenv.exe 的调用刚好出现在安装和卸载的 InstallFinalize 标准操作之前，因此 CustomAction 和 InstallExecuteSequence 表项都可用于这两种情况。  
  
> [!NOTE]
> `devenv /setup`卸载 MSI 包后运行。  
  
 通常，如果将自定义操作添加到 Windows Installer 包，则必须在卸载和回滚过程中处理这些操作。 例如，如果添加自定义操作来自行注册 VSPackage，则必须添加自定义操作对其进行撤消注册。  
  
> [!NOTE]
> 用户可以安装 VSPackage，然后卸载 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 它所集成的的版本。 通过消除运行具有依赖项的代码的自定义操作，可帮助确保 VSPackage 的卸载在该方案中正常工作 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="handling-launch-conditions-at-uninstall-time"></a>在卸载时处理启动条件  
 如果未满足条件，LaunchConditions 标准操作将读取 LaunchCondition 表的行以显示错误消息。 由于启动条件通常用于确保满足系统要求，因此您通常可以在卸载过程中通过将条件添加 `NOT Installed` 到 LaunchCondition 表的 LaunchConditions 行来跳过启动条件。  
  
 另一种方法是添加 `OR Installed` 在卸载过程中不重要的启动条件。 这可确保在卸载过程中条件始终为 true，因此不会显示启动条件错误消息。  
  
> [!NOTE]
> `Installed` 属性 Windows Installer 在检测到已在系统上安装 VSPackage 时设置。  
  
## <a name="see-also"></a>另请参阅  
 [Windows Installer](https://msdn.microsoft.com/187d8965-c79d-4ecb-8689-10930fa8b3b5)   
 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)
