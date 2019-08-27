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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204600"
---
# <a name="elements-of-the-isolated-shell"></a>独立 Shell 的元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以修改注册表设置、 运行时设置和应用程序的独立的 shell 应用程序中，其.vsct、.pkgdef、 and.pkgundef 文件的入口点。  
  
## <a name="registry-settings"></a>注册表设置  
 .Pkgdef 和.pkgundef 文件修改独立的 shell 应用程序的注册表设置。 当运行该应用程序时，按以下顺序定义的注册表设置：  
  
 当运行该应用程序时，按以下顺序定义的注册表设置：  
  
1. 创建应用程序的注册表项。  
  
2. 通过定义指定的项和条目从应用程序的.pkgdef 文件更新注册表。  
  
3. 对于属于你的应用程序的每个包，该包的.pkgdef 文件更新注册表。 每个包由应用程序的.pkgdef 文件中 $RootKey$ \Packages\\{*vsPackageGuid*} 密钥包。  
  
4. 从 AppEnvConfig.pkgdef 和 BaseConfig.pkgdef 中的更新注册表*Visual Studio SDK 安装路径*\Common7\IDE\ShellExtensions\Platform 目录。 这些文件是 Visual Studio 的一部分也是 Visual Studio Shell （独立的模式） 可再发行组件包的一部分。  
  
5. 通过删除指定的项和条目从.pkgundef 文件的应用程序的更新注册表。  
  
## <a name="run-time-settings"></a>运行时间设置  
 当用户启动独立的 shell 应用程序时，它调用的 Visual Studio shell 的启动入口点。 应用程序设置定义你的应用程序启动时，按如下所示：  
  
1. 在 Visual Studio shell 检查特定密钥的应用程序注册表。 如果对启动入口点的调用中指定的键的设置，则该值将覆盖注册表中的值。  
  
2. 如果既没有注册表，也没有入口点参数指定的值的设置，然后使用该设置的默认值。  
  
   当用户从命令行启动你的应用程序时，所有命令行参数将传递给 Visual Studio shell，它会将它们视为相同的 Devenv 的方式处理中。 有关 Devenv 开关的详细信息，请参阅[Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)并[VSPackage 开发的 Devenv 命令行开关](../extensibility/devenv-command-line-switches-for-vspackage-development.md)。 有关如何将包注册的命令行开关的详细信息，请参阅[添加命令行开关](../extensibility/adding-command-line-switches.md)。  
  
## <a name="the-start-entry-point"></a>启动入口点  
 Appenvstub.dll 文件包含用于访问独立的 shell 入口点。 当应用程序启动时，它将调用启动入口点的 Appenvstub.dll。  
  
 可以通过更改传递给启动入口点的最后一个参数的值来更改应用程序的行为。 有关详细信息，请参阅[独立 Shell 入口点参数 (C++)](../extensibility/isolated-shell-entry-point-parameters-cpp.md)。  
  
## <a name="the-vsct-file"></a>。Vsct 文件  
 .Vsct 文件允许您指定哪些标准的 Visual Studio UI 元素是应用程序中可用。 有关详细信息，请参阅[。Vsct 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-vsct-file.md)。  
  
## <a name="the-pkgundef-file"></a>。Pkgundef 文件  
 已安装 Visual Studio 的计算机上安装应用程序时，Visual Studio 注册表项的副本由应用程序。 默认情况下，应用程序使用的计算机已安装的 Vspackage。 .Pkgundef 文件允许你以特定元素的 Visual Studio shell 或扩展的应用程序中删除排除注册表项。 有关详细信息，请参阅[。Pkgundef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 .Pkgundef 文件允许你以特定元素的 Visual Studio shell 或扩展的应用程序中删除排除注册表项。 有关详细信息，请参阅[。Pkgundef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 中列出的包 Guid，可以排除集[包的 Guid 的 Visual Studio 功能](../extensibility/package-guids-of-visual-studio-features.md)。  
  
## <a name="the-pkgdef-file"></a>。Pkgdef 文件  
 .Pkgdef 文件，可以定义应用程序时安装了应用程序设置的注册表项。 .Pkgdef 文件的说明和 Visual Studio shell 使用的注册表项的列表，请参阅[。Pkgdef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)。  
  
## <a name="substitution-strings"></a>替换字符串  
 .Pkgdef 和.pkgundef 文件中使用的替换字符串中列出了[中使用的替换字符串。Pkgdef 和。Pkgundef 文件](../extensibility/substitution-strings-used-in-dot-pkgdef-and-dot-pkgundef-files.md)。  
  
## <a name="other-settings"></a>其他设置  
 如果独立的 shell 应用程序依赖于 Microsoft.VisualStudio.GraphModel.dll，需要将以下绑定重定向添加到独立 Shell 应用程序的.config 文件：  
  
```  
<dependentAssembly>  
    <assemblyIdentity name="Microsoft.VisualStudio.GraphModel" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />  
    <bindingRedirect oldVersion="11.0.0.0" newVersion="12.0.0.0"/>  
</dependentAssembly>  
  
```
