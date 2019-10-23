---
title: 卸载具有 Windows Installer 的 VSPackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a8e92937e848d124c18dc91b9bdfa0f020f27f20
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722131"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
在大多数情况下，Windows Installer 只需通过 "撤消" 安装 VSPackage 的操作即可卸载你的 VSPackage。 还必须在卸载后运行的[命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)中讨论的自定义操作。 由于对 InstallFinalize 标准操作的调用刚好在安装和卸载的标准操作之前发生，因此 CustomAction 和 InstallExecuteSequence 表条目都适用于这两种情况。

> [!NOTE]
> 卸载 MSI 包后运行 `devenv /setup`。

 通常，如果将自定义操作添加到 Windows Installer 包，则必须在卸载和回滚过程中处理这些操作。 例如，如果添加自定义操作来自行注册 VSPackage，则必须添加自定义操作对其进行撤消注册。

> [!NOTE]
> 用户可以安装 VSPackage，然后卸载与之集成的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本。 通过消除在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 上运行依赖项的代码的自定义操作，可帮助确保 VSPackage 的卸载在该方案中工作。

## <a name="handling-launch-conditions-at-uninstall-time"></a>在卸载时处理启动条件
 如果未满足条件，LaunchConditions 标准操作将读取 LaunchCondition 表的行以显示错误消息。 由于启动条件通常用于确保满足系统要求，因此在卸载过程中通常可以通过将 `NOT Installed` 的条件添加到 LaunchCondition 表的 LaunchConditions 行来跳过启动条件。

 一种替代方法是添加在卸载过程中不重要的 `OR Installed`。 这可确保在卸载过程中条件始终为 true，因此不会显示启动条件错误消息。

> [!NOTE]
> `Installed` 是 Windows Installer 在检测到已在系统上安装 VSPackage 时设置的属性。

## <a name="see-also"></a>请参阅
- [Windows 安装程序](https://msdn.microsoft.com/library/187d8965-c79d-4ecb-8689-10930fa8b3b5)
- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)