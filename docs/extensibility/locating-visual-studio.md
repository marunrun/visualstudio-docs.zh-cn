---
title: 查找 Visual Studio |Microsoft Docs
ms.date: 08/21/2017
ms.topic: conceptual
helpviewer_keywords:
- deployment, VSIX
ms.assetid: 680c3b25-7901-4768-8363-6d1fcd1ea636
ms.author: heaths
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a7187fbcc3e3aca990846176676a47f5d17aaf00
ms.sourcegitcommit: 62f42113ae4dae1ddfff1c4e02445acc09913445
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2019
ms.locfileid: "64878148"
---
# <a name="locate-visual-studio"></a>找到 Visual Studio

从 Visual Studio 2017 开始，可以安装多个实例的相同版本或甚至版本。 当您想要保持以前安装的同时预览主开发计算机上的新功能时，这非常有用。 由于这些变化，没有单一的环境变量或注册表值可用于查找实例。 相反，可以使用[COM 查询 API](https://msdn.microsoft.com/library/microsoft.visualstudio.setup.configuration.aspx)来查找与您的扩展插件相关的条件的实例。

这是与 NuGet 包可用于本机和托管代码的快速、 只读的 API。

| 代码 | package |
| ---- | --- |
| Native | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Native |
| Managed | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Interop |

您可以找到给定的路径或当前进程的单一实例或枚举所有实例。 请参阅[我们的示例](https://github.com/Microsoft/vs-setup-samples)有关如何查找 Visual Studio 的完整示例。

## <a name="tools"></a>工具

若要查找 Visual Studio 和其他工具在生成环境、 PowerShell 脚本，安装程序和更多方案中，有许多开放源代码工具可以直接使用，也可以随您自己的脚本一起重新发布。

| 项目 | 描述 |
| ------- | ----------- |
| [vswhere](https://github.com/Microsoft/vswhere) | 单个文件本机可执行文件，找到满足条件，例如版本的实例或预发布版本，安装哪种产品，并且工作负荷进行安装。 此外支持查找 Visual Studio 2010 及更高版本，尽管较少的信息返回的用于 Visual Studio 2017 和更高版本。 请参阅[wiki](https://github.com/Microsoft/vswhere/wiki)有关示例。 |
| [VSSetup cmdlet](https://github.com/Microsoft/vssetup.powershell) | 支持的 PowerShell cmdlet 返回可用于查找基于条件与相同的实例作为对象的丰富信息 2.0 和更高版本的_vswhere_并发现更多有关实例的属性。 请参阅[wiki](https://github.com/Microsoft/vssetup.powershell/wiki)有关示例。 |
| [VSIXBootstrapper](https://github.com/Microsoft/vsixbootstrapper) | 自动定位_vsixinstaller 找_，并将传递通过命令行安装 **.vsix*文件。 此功能可在不具有直接查询 Api 支持的安装程序。 请参阅[wiki](https://github.com/Microsoft/vsixbootstrapper/wiki)有关示例。 |

## <a name="see-also"></a>请参阅

* [Visual Studio 2017 安装程序的更改](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup/)
* [启动 Visual Studio 中使用 DTE](launch-visual-studio-dte.md)