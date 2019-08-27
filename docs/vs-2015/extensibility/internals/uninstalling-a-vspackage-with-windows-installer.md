---
title: 卸载使用 Windows 安装程序 VSPackage |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675231"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可以大多数情况下，Windows 安装程序只需通过卸载你的 VSPackage"撤消"像安装你的 VSPackage。 自定义操作中所述[命令，必须将运行后安装](../../extensibility/internals/commands-that-must-be-run-after-installation.md)必须也卸载后运行。 由于指向 devenv.exe 的调用发生之前进行安装和卸载的 InstallFinalize 标准操作，因此 CustomAction 和 InstallExecuteSequence 表项提供两种情况。  
  
> [!NOTE]
> 运行`devenv /setup`卸载 MSI 包后。  
  
 作为一般规则，如果将自定义操作添加到 Windows Installer 包，则必须处理这些操作期间卸载和回滚。 如果添加自定义操作才能自行注册你的 VSPackage，例如，必须添加自定义操作过注销。  
  
> [!NOTE]
> 它是用户可以安装你的 VSPackage，然后卸载版本的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]与它集成。 您可以帮助确保你的 VSPackage 的卸载工作中这种情况下，通过消除运行具有依赖项的代码的自定义操作[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
## <a name="handling-launch-conditions-at-uninstall-time"></a>处理启动条件在卸载时  
 LaunchConditions 标准操作读取 LaunchCondition 表以显示错误的行不满足条件的消息。 启动条件通常用来确保满足系统要求，则可以通常跳过启动条件在卸载期间通过添加条件，如`NOT Installed`，LaunchConditions LaunchCondition 表的行。  
  
 一种替代方法是添加`OR Installed`来启动卸载过程并不重要的条件。 这将确保该条件在卸载期间始终为 true，并且因此不会显示启动条件错误消息。  
  
> [!NOTE]
> `Installed` 是 Windows 安装程序检测到你的 VSPackage 已安装在系统上时将设置的属性。  
  
## <a name="see-also"></a>请参阅  
 [Windows 安装程序](https://msdn.microsoft.com/187d8965-c79d-4ecb-8689-10930fa8b3b5)   
 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)
