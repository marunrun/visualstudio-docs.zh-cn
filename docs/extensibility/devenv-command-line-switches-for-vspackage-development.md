---
title: VSPackage 开发的 Devenv 命令行开关 |Microsoft Docs
ms.date: 12/10/2018
ms.topic: conceptual
helpviewer_keywords:
- /Setup command line switch
- /ResetSkipPkgs command line switch
- /RootSuffix command line switch
- /SafeMode command line switch
- /Splash command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 289f31c503143dc2b992717483f4d8701414e09d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348053"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 开发的 Devenv 命令行开关

Visual Studio 允许开发人员自动执行任务命令行中的，执行时`devenv.exe`，启动 Visual Studio IDE 的文件。

 任务包括：

- 在从 IDE 外部的预配置中部署应用程序。

- 自动使用预设的生成项目的生成设置，或调试配置。

- 在 IDE 之外，在特定配置中，IDE 加载中的所有内容。 此外可以自定义在启动时 IDE。

## <a name="guidelines-for-switches"></a>开关的准则

Visual Studio 文档介绍了用户级`devenv`命令行开关。 有关详细信息，请参阅[Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)。 `devenv`工具还支持用于 VSPackage 开发、 部署和调试的其他命令行开关。

| 命令行开关 | 描述 |
|---------------------| - |
| `/ResetSkipPkgs` | 清除已添加的用户想要避免加载有问题的 Vspackage，请启动 Visual Studio 的所有跳过加载选项。 SkipLoading 标记的状态禁用 VSPackage 加载。 清除这些标记将重新启用 VSPackage 的加载。<br /><br /> 此开关不带参数。 |
| `/RootSuffix` | 启动 Visual Studio 中通过使用备用位置。 通过 Visual Studio SDK 安装程序创建的快捷方式运行以下命令：<br /><br /> `devenv /RootSuffix exp`<br /><br /> 在这种情况下，`exp`标识具有特定的后缀的位置 (例如，`10.0Exp`而不是`10.0`)。 实验实例，可调试的 VSPackage 单独从要用来编写代码的 Visual Studio 的实例。<br /><br /> 此开关可以接受任何字符串，标识已使用 VSRegEx.exe 创建的位置。 有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。 |
| `/SafeMode` | 在安全模式下，加载默认 IDE 和服务将启动 Visual Studio。 `/SafeMode`参数可防止所有第三方 VSPackages 加载 Visual Studio 启动时，确保执行稳定。<br /><br /> 此开关不带参数。 |
| `/Setup` | 强制 Visual Studio 合并描述菜单、 工具栏和命令组从所有可用的 Vspackage 的资源元数据。 只能以管理员身份运行此命令。 <br /><br /> 此开关不带参数。 `devenv /Setup` 命令通常作为安装过程的最后一步给出。 使用`/Setup`开关不会启动 IDE。|
| `/Splash` | 像往常一样，屏幕上，然后显示一条消息框显示在主 IDE 前，显示了 Visual Studio 启动画面。 消息框，您研究初始屏幕 （例如，若要检查的 VSPackage 产品图标）。<br /><br /> 此开关不带参数。 |

## <a name="see-also"></a>请参阅

- [添加命令行开关](../extensibility/adding-command-line-switches.md)
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)