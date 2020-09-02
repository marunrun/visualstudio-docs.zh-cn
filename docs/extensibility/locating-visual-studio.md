---
title: 正在查找 Visual Studio |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "64878148"
---
# <a name="locate-visual-studio"></a>找到 Visual Studio

从 Visual Studio 2017 开始，你可以安装相同版本甚至版本的多个实例。 当您想要在主开发计算机上预览新功能，同时保留以前的安装时，这非常有用。 由于这些更改，因此没有可用于查找实例的单一环境变量或注册表值。 相反，可以使用 [COM 查询 API](https://msdn.microsoft.com/library/microsoft.visualstudio.setup.configuration.aspx) 基于与扩展相关的条件来查找实例。

这是一个快速的只读 API，其中包含适用于本机和托管代码的 NuGet 包。

| 代码 | 包 |
| ---- | --- |
| 本机 | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Native |
| 托管 | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Interop |

您可以查找给定路径或当前进程的单个实例，或者枚举所有实例。 有关如何查找 Visual Studio 的完整示例，请参阅 [示例](https://github.com/Microsoft/vs-setup-samples) 。

## <a name="tools"></a>工具

若要在生成环境、PowerShell 脚本、安装程序以及更多方案中查找 Visual Studio 和其他工具，可以直接使用多个开源工具，也可以使用自己的脚本进行重新分发。

| 项目 | 说明 |
| ------- | ----------- |
| [vswhere](https://github.com/Microsoft/vswhere) | 单个文件本机可执行文件，用于查找满足条件的实例、发布或预发行的实例、安装的产品以及安装的工作负载。 还支持查找 Visual Studio 2010 和更高版本，但对于 Visual Studio 2017 和更高版本，则返回更少的信息。 有关示例，请参阅 [wiki](https://github.com/Microsoft/vswhere/wiki) 。 |
| [Vssetup.powershell cmdlet](https://github.com/Microsoft/vssetup.powershell) | PowerShell cmdlet 支持2.0 和更高版本，以对象的形式返回丰富信息，你可以使用这些对象基于与 _vswhere_ 相同的条件查找实例，并发现有关实例的更多属性。 有关示例，请参阅 [wiki](https://github.com/Microsoft/vssetup.powershell/wiki) 。 |
| [VSIXBootstrapper](https://github.com/Microsoft/vsixbootstrapper) | 自动查找 _VSIXInstaller_ ，并通过传递命令行来安装 **.vsix* 文件。 此功能在不直接支持查询 Api 的安装程序中很有用。 有关示例，请参阅 [wiki](https://github.com/Microsoft/vsixbootstrapper/wiki) 。 |

## <a name="see-also"></a>另请参阅

* [Visual Studio 2017 安装程序的更改](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup/)
* [使用 DTE 启动 Visual Studio](launch-visual-studio-dte.md)