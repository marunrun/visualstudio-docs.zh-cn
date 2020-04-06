---
title: 添加命令行开关 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f2df3a704c34d97c9d5acfa72249fe492b7f812
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740163"
---
# <a name="add-command-line-switches"></a>添加命令行交换机
您可以在执行*devenv.exe*时添加应用于 VSPackage 的命令行开关。 用于<xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute>声明交换机的名称及其属性。 在此示例中，MySwitch 开关被添加到名为**AddCommandSwitchPackage**的 VSPackage 子类，该子类没有参数，并且自动加载 VSPackage。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 命名参数显示在以下说明中。

||||
|-|-|-|-|
| 参数 | 描述|
| 自变量 | 交换机的参数数。 可以是"*"，也可以是参数列表。 |
| 需求负载 | 如果设置为 1，则自动加载 VS 包，否则设置为 0。 |
| 帮助字符串 | 要用**devenv /？** 显示的字符串的帮助字符串或资源 ID。 |
| 名称 | 开关。 |
| 包装吉德 | 包的 GUID。 |

 参数的第一个值通常是 0 或 1。 特殊值"*"可用于指示命令行的整个其余部分是参数。 这对于用户必须传递调试器命令字符串的调试方案非常有用。

 DemandLoad 值为`true`（1）`false`或 （0）表示应自动加载 VS 包。

 HelpString 值是显示在**devenv /？** 帮助显示。 此值应以"#nnn"的形式，其中 nnn 是整数。 资源文件中的字符串值应以新的行字符结尾。

 Name 值是交换机的名称。

 包吉德值是实现此交换机的包的 GUID。 IDE 使用此 GUID 在命令行交换机适用的注册表中查找 VSPackage。

## <a name="retrieve-command-line-switches"></a>检索命令行交换机
 加载包后，可以通过完成以下步骤来检索命令行开关。

1. 在 VSPackage 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>实现中，`QueryService`调用<xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine>以获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>接口。

2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A>以检索用户输入的命令行交换机。

   以下代码演示如何查找用户是否输入了 MySwitch 命令行交换机：

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 您有责任在每次加载包时检查命令行交换机。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
- [创建PkgDef实用程序](../extensibility/internals/createpkgdef-utility.md)
- [.Pkgdef 文件](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
