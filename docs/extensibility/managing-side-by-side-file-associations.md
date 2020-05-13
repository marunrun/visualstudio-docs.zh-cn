---
title: 管理并行文件关联 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c284fe7ef4c2d07051a8524860583cb634e13bf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702765"
---
# <a name="manage-side-by-side-file-associations"></a>管理并行文件关联

如果 VSPackage 提供文件关联，则必须决定如何处理应调用 的特定[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本的并行安装来打开文件。 不兼容的文件格式使问题复杂化。

用户希望产品的新版本与早期版本兼容，以便可以在新版本中加载现有文件，而不会丢失数据。 理想情况下，VSPackage 可以加载和保存早期版本的文件格式。 如果事实并非如此，则应提供将文件格式升级到新版本的 VSPackage。 此方法的缺点是无法在早期版本中打开升级的文件。

为了避免此问题，您可以在文件格式变得不兼容时更改扩展名。 例如，VSPackage 的版本 1 可以使用扩展 *.mypkg10，* 版本 2 可以使用扩展 *.mypkg20*。 此差异标识打开特定文件的 VSPackage。 如果将较新的 VSPackage 添加到与旧扩展名关联的程序列表中，用户可以右键单击该文件，并选择在较新的 VSPackage 中打开该文件。 此时，您的 VSPackage 可以提供将文件升级到新格式或打开文件并保持与早期版本的 VSPackage 的兼容性。

> [!NOTE]
> 您可以组合这些方法。 例如，您可以通过加载较旧的文件提供向后兼容性，并在用户保存文件格式时提供升级文件格式。

## <a name="face-the-problem"></a>面对问题

如果希望多个并行 VSPackages 使用相同的扩展，则必须选择与扩展关联的版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 下面是两个备选方案：

- 在用户计算机上安装的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]最新版本中打开该文件。

   在此方法中，安装程序负责确定 最新版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，包括为文件关联编写的注册表项中的最新版本。 在 Windows 安装程序包中，可以包括自定义操作来设置指示 最新版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的属性。

  > [!NOTE]
  > 在此上下文中，"最新"表示"最新支持的版本"。 这些安装程序条目不会自动检测 的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]后续版本。 [检测系统要求](../extensibility/internals/detecting-system-requirements.md)和[安装后必须运行的命令](../extensibility/internals/commands-that-must-be-run-after-installation.md)中的条目与此处介绍的条目类似，并且需要支持 的其他[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本。

   自定义操作表中的以下行将DEVENV_EXE_LATEST属性设置为由安装[后必须在命令](../extensibility/internals/commands-that-must-be-run-after-installation.md)中讨论的 AppSearch 和 RegLocator 表设置的属性。 安装执行序列表中的行在执行序列的早期计划自定义操作。 "条件"列中的值使逻辑工作：

  - Visual Studio .NET 2002 是最新版本，如果它是唯一的当前版本。

  - Visual Studio .NET 2003 是最新版本，仅当它存在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]且不存在时。

  - [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]是最新版本，如果它是唯一的当前版本。

    最终结果是，DEVENV_EXE_LATEST包含最新版本 devenv.exe 的路径。

  **自定义操作表行，确定最新版本的可视化工作室**

  |操作|类型|源|目标|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **安装确定最新版本的可视化工作室的执行序列表行**

  |操作|条件|序列|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002与未（DEVENV_EXE_2003或DEVENV_EXE_2005）|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003，而不是DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   您可以使用 Windows 安装程序包注册表表中的DEVENV_EXE_LATEST属性编写**HKEY_CLASSES_ROOT*ProgId*ShellOpenCommand**键的默认值 [DEVENV_EXE_LATEST] "%1"

- 运行一个共享启动程序，可以从可用的 VSPackage 版本做出最佳选择。

   的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]开发人员选择这种方法来处理多种格式的解决方案和项目的复杂需求，这些解决方案和项目来自许多版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 在此方法中，您将启动程序注册为扩展处理程序。 启动程序检查该文件，并决定哪个版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，您的 VSPackage 可以处理该特定文件。 例如，如果用户打开上次由 VSPackage 的特定版本保存的文件，启动器可以在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的匹配版本中启动该 VSPackage。 此外，用户可以将启动器配置为始终启动最新版本。 启动器还可以提示用户升级文件的格式。 如果文件的格式包含版本号，则启动器可以通知用户文件格式是否来自版本，该版本晚于一个或多个已安装的 VS 包。

   启动器应位于 Windows 安装程序组件中，该组件与 VSPackage 的所有版本共享。 此过程可确保始终安装最新版本，并且在卸载 VSPackage 的所有版本之前不会被删除。 这样，即使卸载了一个版本的 VSPackage，也会保留启动组件的文件关联和其他注册表项。

## <a name="uninstall-and-file-associations"></a>卸载和文件关联

卸载为文件关联写入注册表项的 VS 包将删除文件关联。 因此，扩展没有关联的程序。 Windows 安装程序不会"恢复"安装 VSPackage 时添加的注册表项。 以下是修复用户文件关联的一些方法：

- 使用前面描述的共享启动组件。

- 指示用户运行用户希望拥有文件关联的 VSPackage 版本的修复。

- 提供单独的可执行程序，以重写相应的注册表项。

- 提供配置选项页或对话框，允许用户选择文件关联并回收丢失的关联。 指示用户在卸载后运行它。

## <a name="see-also"></a>请参阅

- [注册并行部署的文件名扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [注册文件名扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
