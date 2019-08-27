---
title: 添加命令行开关 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e28a3f303849458a407b212d3aad1a8c198f6d25
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562271"
---
# <a name="adding-command-line-switches"></a>添加命令行开关
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以添加执行 devenv.exe 时应用于你的 VSPackage 的命令行开关。 使用<xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute>声明的开关和其属性的名称。 在此示例中，MySwitch 的交换机添加为子类名为 VSPackage **AddCommandSwitchPackage**不带任何参数且会自动加载 VSPackage。  
  
```csharp  
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]  
```  
  
 下表中所示命名的参数  
  
 自变量  
 开关的参数数目。 可以是"*"，或自变量的列表。  
  
 DemandLoad  
 如果此值设置为 1，否则设置为 0，则会自动加载 VSPackage。  
  
 HelpString  
 帮助字符串或资源 ID 的字符串以显示与**devenv /？**。  
  
 名称  
 开关。  
  
 PackageGuid  
 包的 GUID。  
  
 第一个参数的值通常为 0 或 1。 特殊值 * 可用于指示整个命令行的其余部分是自变量。 这可用于调试的方案，用户必须通过在调试器命令字符串中。  
  
 DemandLoad 值是`true`(1) 或`false`(0) 指示应自动加载 VSPackage。  
  
 HelpString 值是在 devenv 中显示的字符串的资源 ID /？帮助显示。 此值应在窗体"#nnn"其中 nnn 是一个整数。 在资源文件中的字符串值应以新行字符结尾。  
  
 名称值是交换机的名称。  
  
 PackageGuid 值为实现此开关的包的 GUID。 IDE 使用此 GUID 在命令行开关适用的注册表中找到 VSPackage。  
  
## <a name="retrieving-command-line-switches"></a>检索命令行开关  
 加载包时，可以通过完成以下步骤检索的命令行开关。  
  
1. 在你的 VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>实现中，调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine>若要获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>接口。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A>来检索用户输入的命令行开关。  
  
   下面的代码演示如何找出是否由用户输入 MySwitch 命令行开关：  
  
```csharp  
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));  
  
int isPresent = 0;  
string optionValue = "";  
  
cmdline.GetOption("MySwitch", out isPresent, out optionValue);  
```  
  
 它由你负责每次加载包时检查命令行开关。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)   
 [CreatePkgDef 实用工具](../extensibility/internals/createpkgdef-utility.md)   
 [.Pkgdef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)
