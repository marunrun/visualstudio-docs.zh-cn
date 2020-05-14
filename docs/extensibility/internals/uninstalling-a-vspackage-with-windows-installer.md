---
title: 使用 Windows 安装程序卸载 VS 包 |微软文档
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
ms.openlocfilehash: fee88e895d40d42114eaf53422503524594b485f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704276"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
在大多数情况下，Windows 安装程序只需"撤消"安装 VSPackage 时所做的"撤消"即可卸载您的 VSPackage。 [安装后必须运行的命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)中讨论的自定义操作也必须在卸载后运行。 由于对 devenv.exe 的调用发生在安装和卸载的"安装Finalize"标准操作之前，因此自定义操作和安装执行顺序表条目同时适用于这两种情况。

> [!NOTE]
> 卸载`devenv /setup`MSI 包后运行。

 通常，如果将自定义操作添加到 Windows 安装程序包，则必须在卸载和回滚期间处理这些操作。 例如，如果将自定义操作添加到自动注册 VSPackage，则还必须添加自定义操作来取消注册它。

> [!NOTE]
> 用户可以安装 VSPackage，然后卸载与其集成的版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 通过消除运行具有依赖项的代码的自定义操作，可以帮助确保 VSPackage 的卸载在这种情况下有效[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="handling-launch-conditions-at-uninstall-time"></a>卸载时处理启动条件
 启动条件标准操作读取启动条件表的行，以在不符合条件时显示错误消息。 由于启动条件通常用于确保满足系统要求，因此通常可以通过将条件`NOT Installed`添加到启动条件表的启动条件行来跳过卸载期间的启动条件。

 另一种方法是在卸载`OR Installed`期间添加不重要的启动条件。 这可确保在卸载期间条件始终为 true，因此不会显示启动条件错误消息。

> [!NOTE]
> `Installed`是 Windows 安装程序在检测到您的 VSPackage 已安装在系统上时设置的属性。

## <a name="see-also"></a>请参阅
- [Windows 安装程序](https://msdn.microsoft.com/library/187d8965-c79d-4ecb-8689-10930fa8b3b5)
- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)
