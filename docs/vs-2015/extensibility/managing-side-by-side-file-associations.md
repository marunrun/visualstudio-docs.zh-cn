---
title: 管理并行文件关联 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b8ca68aec180c51a170fd6ecce58237a5b306705
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194392"
---
# <a name="managing-side-by-side-file-associations"></a>管理并行文件关联

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你的 VSPackage 提供文件关联，你必须确定如何处理并行安装，其中应该调用特定版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 来打开文件。 不兼容的文件格式将问题组合在一起。

用户希望新版本的产品与早期版本兼容，以便在不丢失数据的情况下，在新版本中加载现有文件。 理想情况下，VSPackage 可以加载并保存早期版本的文件格式。 如果不是这样，则应提供将文件格式升级到 VSPackage 的新版本。 此方法的缺点是升级后的文件无法在早期版本中打开。

若要避免此问题，可以在文件格式不兼容时更改扩展。 例如，VSPackage 的版本1可以使用扩展名 mypkg10，版本2可以使用扩展名 mypkg20。 此差异标识打开特定文件的 VSPackage。 如果将较新的 Vspackage 添加到与旧扩展关联的程序列表中，用户可以右键单击该文件，然后选择在较新的 VSPackage 中打开它。 此时，你的 VSPackage 可以提供将文件升级到新格式或打开该文件，并保持与早期版本的 VSPackage 的兼容性。

> [!NOTE]
> 可以组合这些方法。 例如，你可以通过加载较旧的文件并提供在用户保存文件格式时进行升级来提供向后兼容性。

## <a name="facing-the-problem"></a>面临的问题

如果希望多个并行 Vspackage 使用同一扩展，则必须选择 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 与该扩展关联的版本。 下面是两种备选方案：

- 在用户计算机上安装的最新版本中打开该文件 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

   在此方法中，安装程序负责确定的最新版本， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 并将其包括在为文件关联编写的注册表项中。 在 Windows Installer 包中，可以包含自定义操作，以设置指示最新版本的属性 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

  > [!NOTE]
  > 在此上下文中，"最新" 指的是 "支持的最新版本"。 这些安装程序项不会自动检测的后续版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 [检测系统要求](../extensibility/internals/detecting-system-requirements.md)以及在[安装后必须运行的命令](../extensibility/internals/commands-that-must-be-run-after-installation.md)中的条目类似于此处提供的条目，并且需要支持的其他版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

   CustomAction 表中的以下行将 DEVENV_EXE_LATEST 属性设置为由 [必须在安装后运行的命令](../extensibility/internals/commands-that-must-be-run-after-installation.md)中讨论的 AppSearch 和 RegLocator 表所设置的属性。 InstallExecuteSequence 表中的行在执行顺序初期计划自定义操作。 "条件" 列中的值使逻辑工作：

  - 如果是最新版本，则 Visual Studio .NET 2002 是最新版本。

  - 仅当 Visual Studio .NET 2003 存在且不存在时，它才是最新版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

  - [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 是最新版本（如果它是唯一的版本）。

    最终结果是 DEVENV_EXE_LATEST 包含 devenv.exe 的最新版本的路径。

  **确定 Visual Studio 最新版本的 CustomAction 表行**

  |操作|类型|Source|目标|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **确定 Visual Studio 最新版本的 InstallExecuteSequence 表行**

  |操作|条件|序列|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 不 (DEVENV_EXE_2003 或 DEVENV_EXE_2005) |410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 且不 DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   您可以使用 Windows Installer 包的注册表表中的 DEVENV_EXE_LATEST 属性来写入 HKEY_CLASSES_ROOT*ProgId*ShellOpenCommand 密钥的默认值 [DEVENV_EXE_LATEST] "%1"

- 运行共享启动器程序，以便从可用的 VSPackage 版本中做出最佳选择。

   开发人员 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 选择此方法来处理多种版本的解决方案和项目的复杂需求 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 在此方法中，将启动器程序注册为扩展处理程序。 启动器会检查文件，并决定哪个版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和你的 VSPackage 可以处理该特定文件。 例如，如果用户打开了由 VSPackage 的特定版本最后保存的文件，则启动器可以在的匹配版本中启动该 VSPackage [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 此外，用户还可以将启动器配置为始终启动最新版本。 启动器还可能会提示用户升级文件的格式。 如果该文件的格式包含版本号，则如果文件格式来自于一个或多个已安装的 Vspackage 版本，则启动器可能会通知用户。

   启动器应位于与 VSPackage 的所有版本共享的 Windows Installer 组件中。 此过程可确保始终安装最新版本，并且在卸载 VSPackage 的所有版本之前，不会将其删除。 这样，即使卸载了某个版本的 VSPackage，也会保留启动器组件的文件关联和其他注册表项。

## <a name="uninstall-and-file-associations"></a>卸载和文件关联

卸载为文件关联写入注册表项的 VSPackage 将删除文件关联。 因此，该扩展没有关联的程序。 Windows Installer 不会 "恢复" 安装 VSPackage 时添加的注册表项。 以下是修复用户文件关联的一些方法：

- 如前文所述，使用共享启动器组件。

- 指示用户运行用户想要拥有文件关联的 VSPackage 的版本修复。

- 提供一个单独的可执行程序，用于重写相应的注册表项。

- 提供 "配置选项" 页或对话框，使用户可以选择文件关联并回收丢失的关联。 指示用户在卸载后运行该命令。

## <a name="see-also"></a>另请参阅

[为并行部署](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) 
 注册文件扩展名正在[为文件扩展名注册谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
