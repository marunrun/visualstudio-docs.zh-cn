---
title: 管理通过并行文件关联 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194392"
---
# <a name="managing-side-by-side-file-associations"></a>管理并行文件关联

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你的 VSPackage 提供文件关联，则必须确定如何处理通过并行安装在其中的某个特定版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]应被调用来打开文件。 文件格式不兼容复合问题。

用户期望的产品可与早期版本兼容，以便可以不会丢失数据的新版本中加载现有文件的新版本。 理想情况下，你的 VSPackage 可以同时加载和保存的早期版本的文件格式。 如果不为 true，你应提供要升级到你的 VSPackage 的新版本的文件格式。 这种方法的缺点是不能在早期版本中打开该升级后的文件。

若要避免此问题，可以更改扩展时文件格式变得不兼容。 例如，版本 1 的你的 VSPackage 可以使用扩展、.mypkg10 和版本 2 可以使用扩展，.mypkg20。 这种差异标识打开特定文件的 VSPackage。 如果将较新的 Vspackage 添加到与旧扩展相关联的程序列表中，用户可以右键单击该文件，然后选择以更高版本的 VSPackage 中打开它。 此时，你的 VSPackage 可提供的用于升级到新的格式的文件或打开文件并保持与早期版本的 VSPackage 的兼容性。

> [!NOTE]
> 你可以组合使用这些方法。 例如，可通过加载较旧的文件提供向后兼容性，并提供要升级的文件格式时用户将其保存。

## <a name="facing-the-problem"></a>面向问题

如果希望多个并行的 Vspackage，使用相同的扩展名，则必须选择的版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]与扩展相关联。 下面是两个替代方法：

- 打开的最新版本中的文件[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]用户的计算机上安装。

   在这种方法，您的安装程序是负责确定的最新版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]和包含在编写的文件关联的注册表项。 可以在 Windows Installer 包中，包含要设置一个属性，指示的最新版本的自定义操作[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

  > [!NOTE]
  > 在此上下文中，"最新"意味着"最新支持的版本。" 这些安装程序条目将不会自动检测的后续版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 中的条目[检测系统要求](../extensibility/internals/detecting-system-requirements.md)并在[命令，必须将运行安装后](../extensibility/internals/commands-that-must-be-run-after-installation.md)是类似于本文中介绍的并且需要用来支持其他版本的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

   CustomAction 表中的以下行设置 DEVENV_EXE_LATEST 属性是由 AppSearch 设置的属性和 RegLocator 表中所述[命令，必须将运行安装后](../extensibility/internals/commands-that-must-be-run-after-installation.md)。 InstallExecuteSequence 表中的行计划执行顺序中尽早的自定义操作。 条件列进行的逻辑工作中的值：

  - Visual Studio.NET 2002年是最新版本，如果它是仅存在版本。

  - 仅当存在时，visual Studio.NET 2003年是最新版本和[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]不存在。

  - [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 如果它是仅存在版本，是最新版本。

    最终结果是 DEVENV_EXE_LATEST 包含 devenv.exe 的最新版本的路径。

  **确定最新版本的 Visual Studio 的 CustomAction 表行**

  |操作|类型|Source|Target|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **确定最新版本的 Visual Studio 的 InstallExecuteSequence 表行**

  |操作|条件|序列|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 和 NOT （DEVENV_EXE_2003 或 DEVENV_EXE_2005）|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 和不 DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   可以使用 Windows Installer 包的注册表表中的 DEVENV_EXE_LATEST 属性编写 HKEY_CLASSES_ROOT*ProgId*ShellOpenCommand 键的默认值，[DEVENV_EXE_LATEST]"%1"

- 运行共享的启动器程序，以便从可用的 VSPackage 版本的最佳选择。

   开发人员[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]选择此方法来处理复杂的多个格式的解决方案和项目所产生的多个版本的要求[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 在此方法中，启动器程序注册为扩展处理程序。 启动程序检查该文件，并决定哪个版本的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]和你的 VSPackage 可以处理该特定文件。 例如，如果用户打开上次保存你的 VSPackage 的特定版本的文件，启动器可以启动该 VSPackage 中的匹配版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 此外，用户可以配置启动器始终启动最新版本。 启动程序还可能提示用户升级文件的格式。 如果文件的格式包含一个版本号，启动器可以通知用户，如果文件格式是从版本晚于一个或多个已安装的 Vspackage。

   启动器应为与你的 VSPackage 的所有版本共享一个 Windows 安装程序组件。 此过程可确保最新版本始终安装和卸载你的 VSPackage 的所有版本才会删除。 这种方式，文件关联和启动程序组件的其他注册表项会保留即使在卸载 VSPackage 的一个版本。

## <a name="uninstall-and-file-associations"></a>卸载和文件关联

卸载 VSPackage 写入文件关联的注册表项中删除的文件关联。 因此，扩展具有任何关联的节目。 Windows 安装程序未"恢复"安装 VSPackage 时添加的注册表项。 下面是修复用户的文件关联的一些方法：

- 使用共享的启动器组件，如前面所述。

- 指示用户运行版本的用户想要拥有的文件关联的 VSPackage 的修复。

- 提供了单独的可执行程序，用于重写相应的注册表项。

- 提供配置选项的页面或对话框框中，可让用户选择文件关联和回收丢失的关联。 指示用户在卸载后运行。

## <a name="see-also"></a>请参阅

[通过并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
[注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
