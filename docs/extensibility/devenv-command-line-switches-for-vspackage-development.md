---
title: 用于 VSPackage 开发的 Devenv 命令线交换机 |微软文档
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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad3a5125a730b9230959bbf9342b4c0a4823c4d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712195"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>用于 VSPackage 开发的 Devenv 命令行交换机

可视化工作室允许开发人员在执行启动`devenv.exe`Visual Studio IDE 的文件时自动执行命令行的任务。

 任务包括：

- 从 IDE 外部部署预设计配置中的应用程序。

- 使用预设生成设置或调试配置自动生成项目。

- 在特定配置中加载 IDE，全部来自 IDE 外部。 您还可以在启动时自定义 IDE。

## <a name="guidelines-for-switches"></a>开关指南

Visual Studio 文档描述了用户级`devenv`命令行交换机。 有关详细信息，请参阅[Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)。 该工具`devenv`还支持其他命令行交换机，这些开关对 VSPackage 开发、部署和调试非常有用。

| 命令行开关 | 描述 |
|---------------------| - |
| `/ResetSkipPkgs` | 清除希望避免加载有问题的 VS 包的用户添加的所有跳过加载选项，然后启动 Visual Studio。 跳过加载标记的存在会禁用 VSPackage 的加载。 清除标记可重新启用 VSPackage 的加载。<br /><br /> 此开关不带参数。 |
| `/RootSuffix` | 使用备用位置启动可视化工作室。 以下命令由 Visual Studio SDK 安装程序创建的快捷方式运行：<br /><br /> `devenv /RootSuffix exp`<br /><br /> 在这种情况下，`exp`标识具有特定后缀的位置（例如，`10.0Exp`而不是`10.0`。 实验实例允许您将 VSPackage 与用于编写代码的 Visual Studio 实例分开调试。<br /><br /> 此开关可以采用任何使用 VSRegEx.exe 标识已创建位置的字符串。 有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。 |
| `/SafeMode` | 在安全模式下启动 Visual Studio，仅加载默认 IDE 和服务。 该`/SafeMode`交换机可防止所有第三方 VSPackages 在 Visual Studio 启动时加载，从而确保稳定执行。<br /><br /> 此开关不带参数。 |
| `/Setup` | 强制 Visual Studio 合并资源元数据，这些元数据描述所有可用 VSPackages 中的菜单、工具栏和命令组。 您只能以管理员身份运行此命令。 <br /><br /> 此开关不带参数。 `devenv /Setup` 命令通常作为安装过程的最后一步给出。 使用`/Setup`交换机不会启动 IDE。|
| `/Splash` | 像往常一样显示可视化工作室初始屏幕，然后在显示主 IDE 之前显示一个消息框。 消息框允许您研究初始屏幕（例如，检查 VSPackage 产品图标）。<br /><br /> 此开关不带参数。 |

## <a name="see-also"></a>请参阅

- [添加命令行交换机](../extensibility/adding-command-line-switches.md)
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
