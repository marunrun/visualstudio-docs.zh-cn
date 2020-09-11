---
title: 卸载具有 Windows Installer 的 VSPackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6cdf9023512f4225e2a8edcadcf589cb61547e24
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011809"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
在大多数情况下，Windows Installer 只需通过 "撤消" 安装 VSPackage 的操作即可卸载你的 VSPackage。 还必须在卸载后运行的 [命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md) 中讨论的自定义操作。 由于对 devenv.exe 的调用刚好出现在安装和卸载的 InstallFinalize 标准操作之前，因此 CustomAction 和 InstallExecuteSequence 表项都可用于这两种情况。

> [!NOTE]
> `devenv /setup`卸载 MSI 包后运行。

 通常，如果将自定义操作添加到 Windows Installer 包，则必须在卸载和回滚过程中处理这些操作。 例如，如果添加自定义操作来自行注册 VSPackage，则必须添加自定义操作对其进行撤消注册。

> [!NOTE]
> 用户可以安装 VSPackage，然后卸载 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 它所集成的的版本。 通过消除运行具有依赖项的代码的自定义操作，可帮助确保 VSPackage 的卸载在该方案中正常工作 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="handling-launch-conditions-at-uninstall-time"></a>在卸载时处理启动条件
 如果未满足条件，LaunchConditions 标准操作将读取 LaunchCondition 表的行以显示错误消息。 由于启动条件通常用于确保满足系统要求，因此您通常可以在卸载过程中通过将条件添加 `NOT Installed` 到 LaunchCondition 表的 LaunchConditions 行来跳过启动条件。

 另一种方法是添加 `OR Installed` 在卸载过程中不重要的启动条件。 这可确保在卸载过程中条件始终为 true，因此不会显示启动条件错误消息。

> [!NOTE]
> `Installed` 属性 Windows Installer 在检测到已在系统上安装 VSPackage 时设置。

## <a name="see-also"></a>请参阅
- [Windows Installer](/previous-versions/ee231230(v=vs.100))
- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)