---
title: 独立 Shell 的元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: f8d68c3d-9134-4a8f-b566-485956cd321e
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3a95b7da718f050357f6ecd79c90c389dd6085d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204600"
---
# <a name="elements-of-the-isolated-shell"></a>独立 Shell 的元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以修改独立 shell 应用程序的注册表设置、运行时设置和应用程序入口点，以及其. .vsct、. .pkgdef 和 .pkgundef 文件。  
  
## <a name="registry-settings"></a>注册表设置  
 .Pkgdef 和 .pkgundef 文件都修改了独立 shell 应用程序的注册表设置。 当应用程序运行时，注册表设置的定义顺序如下：  
  
 当应用程序运行时，注册表设置的定义顺序如下：  
  
1. 将创建应用程序的注册表项。  
  
2. 通过定义指定的键和项，从应用程序的 .pkgdef 文件更新注册表。  
  
3. 对于应用程序中的每个包，将从该程序包的 .pkgdef 文件更新注册表。 每个包都在应用程序的 .pkgdef 文件中由包的 $RootKey $ \Packages \\ {*vsPackageGuid*} 键定义。  
  
4. 从 *Visual STUDIO SDK 安装路径*\Common7\IDE\ShellExtensions\Platform 目录中的 AppEnvConfig 和 BaseConfig 更新注册表。 这些文件是 Visual Studio 的一部分，也是 Visual Studio Shell 的一部分 (隔离模式) 可再发行组件包。  
  
5. 通过删除指定的密钥和条目，从应用程序的 .pkgundef 文件更新注册表。  
  
## <a name="run-time-settings"></a>运行时设置  
 当用户启动独立 shell 应用程序时，它将调用 Visual Studio shell 的开始入口点。 应用程序设置是在应用程序启动时定义的，如下所示：  
  
1. Visual Studio shell 检查应用程序注册表中的特定项。 如果在对开始入口点的调用中指定了某个键的设置，则该值将覆盖注册表中的值。  
  
2. 如果注册表和入口点参数都不指定设置的值，则使用该设置的默认值。  
  
   当用户从命令行启动应用程序时，会将所有命令行开关传递到 Visual Studio shell，并以 Devenv 的相同方式对待它们。 有关 Devenv 开关的详细信息，请参阅 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md) 和 [Devenv 命令行开关，用于 VSPackage 开发](../extensibility/devenv-command-line-switches-for-vspackage-development.md)。 有关包如何注册命令行开关的详细信息，请参阅 [添加命令行开关](../extensibility/adding-command-line-switches.md)。  
  
## <a name="the-start-entry-point"></a>起始入口点  
 Appenvstub.dll 文件包含用于访问独立 shell 的入口点。 当应用程序启动时，它将调用 Appenvstub.dll 的开始入口点。  
  
 可以通过更改传递到开始入口点的最后一个参数的值来更改应用程序的行为。 有关详细信息，请参阅 [独立 Shell 入口点参数 (c + +) ](../extensibility/isolated-shell-entry-point-parameters-cpp.md)。  
  
## <a name="the-vsct-file"></a>此..Vsct 文件  
 使用 .vsct 文件可以指定哪些标准 Visual Studio UI 元素在应用程序中可用。 有关详细信息，请参阅 [。.Vsct 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-vsct-file.md)。  
  
## <a name="the-pkgundef-file"></a>此..Pkgundef 文件  
 如果在已安装 Visual Studio 的计算机上安装了应用程序，则会为该应用程序创建 Visual Studio 注册表项的副本。 默认情况下，应用程序使用计算机上已安装的 Vspackage。 .Pkgundef 文件允许你排除注册表项，以便删除应用程序中的 Visual Studio shell 或扩展的特定元素。 有关详细信息，请参阅 [。.Pkgundef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 .Pkgundef 文件允许你排除注册表项，以便删除应用程序中的 Visual Studio shell 或扩展的特定元素。 有关详细信息，请参阅 [。.Pkgundef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 [Visual Studio 功能的 "包 guid](../extensibility/package-guids-of-visual-studio-features.md)" 中列出了可以排除的包 guid 集。  
  
## <a name="the-pkgdef-file"></a>此..Pkgdef 文件  
 .Pkgdef 文件允许你定义安装应用程序时设置的应用程序的注册表项。 有关 .pkgdef 文件的说明以及 Visual Studio shell 使用的注册表项列表，请参阅 [。.Pkgdef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)。  
  
## <a name="substitution-strings"></a>替换字符串  
 在 [中使用的替换字符串中列出了 .pkgdef 和 .pkgundef 文件中使用的替换字符串。.Pkgdef 和。.Pkgundef 文件](../extensibility/substitution-strings-used-in-dot-pkgdef-and-dot-pkgundef-files.md)。  
  
## <a name="other-settings"></a>其他设置  
 如果你的独立 shell 应用程序依赖于 Microsoft.VisualStudio.GraphModel.dll，则需要将以下绑定重定向添加到你的独立 Shell 应用程序的 .config 文件中：  
  
```  
<dependentAssembly>  
    <assemblyIdentity name="Microsoft.VisualStudio.GraphModel" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />  
    <bindingRedirect oldVersion="11.0.0.0" newVersion="12.0.0.0"/>  
</dependentAssembly>  
  
```
