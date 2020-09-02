---
title: 添加命令行开关 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: bb4abf5352ac6ad78852bd3224df0b22784470db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903482"
---
# <a name="add-command-line-switches"></a>添加命令行开关
执行 *devenv.exe* 时，可以添加适用于 VSPackage 的命令行开关。 使用 <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute> 声明开关的名称及其属性。 在此示例中，为名为 **AddCommandSwitchPackage** 的 VSPackage 的子类添加了 MySwitch 开关，其中不包含参数，并且 VSPackage 会自动加载。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 以下说明显示了命名参数。

|名称|说明|
|-|-|
| 参数 | 开关的参数数目。 可以是 "*"，也可以是参数列表。 |
| DemandLoad | 如果此设置为1，则自动加载 VSPackage，否则设置为0。 |
| HelpString | 要用 **devenv/？** 显示的字符串的帮助字符串或资源 ID。 |
| 名称 | 开关。 |
| PackageGuid | 包的 GUID。 |

 参数的第一个值通常为0或1。 特殊值 "*" 可用于指示命令行的整个余数是参数。 这对于调试用户必须传入调试器命令字符串的方案非常有用。

 DemandLoad 值为 `true` (1) 或 `false` (0) 指示应自动加载 VSPackage。

 HelpString 值是在**devenv/？** 中显示的字符串的资源 ID。 帮助显示。 此值的形式应为 "#nnn"，其中 nnn 是整数。 资源文件中的字符串值应以换行符结尾。

 Name 值是交换机的名称。

 PackageGuid 值是实现此开关的包的 GUID。 IDE 使用此 GUID 在注册表中查找应用命令行开关的 VSPackage。

## <a name="retrieve-command-line-switches"></a>检索命令行开关
 加载包时，可以通过完成以下步骤来检索命令行开关。

1. 在 VSPackage 的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 实现中，调用 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> 以获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> 接口。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> 以检索用户输入的命令行开关。

   下面的代码演示如何确定用户是否输入了 MySwitch 命令行开关：

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 每次加载包时都需要检查命令行开关。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
- [CreatePkgDef 实用程序](../extensibility/internals/createpkgdef-utility.md)
- [..Pkgdef 文件](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
