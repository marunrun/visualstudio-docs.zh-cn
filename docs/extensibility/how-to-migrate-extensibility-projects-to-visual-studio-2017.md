---
title: 如何：将扩展性项目迁移到 Visual Studio 2017 |Microsoft Docs
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 01c0c8613ec2e4fe72613867d623d510d9734e45
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917658"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>如何：将扩展性项目迁移到 Visual Studio 2017

本文档介绍如何将扩展性项目升级到 Visual Studio 2017。 除了介绍如何更新项目文件以外，还介绍了如何从扩展清单版本2（VSIX v2）升级到新版本 3 VSIX 清单格式（VSIX v3）。

## <a name="install-visual-studio-2017-with-required-workloads"></a>安装包含所需工作负荷的 Visual Studio 2017

请确保您的安装包括以下工作负载：

* .NET 桌面开发
* Visual Studio 扩展开发

## <a name="open-vsix-solution-in-visual-studio-2017"></a>在 Visual Studio 2017 中打开 VSIX 解决方案

所有 VSIX 项目都需要升级到 Visual Studio 2017 的主要版本单向升级。

将更新项目文件（例如 * *.csproj*）：

* I o n-现设置为15。0
* OldToolsVersion （如果之前存在）-现设置为14。0

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>更新 VSSDK. BuildTools NuGet 包

> [!Note]
> 如果解决方案未引用 VSSDK BuildTools NuGet 包，则可以跳过此步骤。

若要在新的 VSIX v3 （版本3）格式中生成扩展，你的解决方案将需要通过新的 VSSDK 生成工具生成。 这将与 Visual Studio 2017 一起安装，但 VSIX v2 扩展可能会通过 NuGet 保存对较旧版本的引用。 如果是这样，你将需要为你的解决方案手动安装 VSSDK NuGet 包的更新。

若要更新对 VSSDK 的 NuGet 引用，请执行以下操作：

* 右键单击解决方案，然后选择 "**管理解决方案的 NuGet 包**"。
* 导航到 "**更新**" 选项卡。
* 选择**VSSDK. BuildTools （最新版本）** 。
* 按 "**更新**"。

![VSSDK 生成工具](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>对 VSIX 扩展清单进行更改

若要确保用户的 Visual Studio 安装具有运行扩展所需的所有程序集，请指定扩展清单文件中的所有必备组件或包。 当用户尝试安装扩展时，VSIXInstaller 将检查是否安装了所有必备组件。 如果缺少某些组件，系统将提示用户安装所缺少的组件，作为扩展安装过程的一部分。

> [!Note]
> 所有扩展插件应该至少指定 Visual Studio 核心编辑器组件作为必备组件。

* 编辑扩展清单文件（通常称为*source.extension.vsixmanifest*）。
* 确保 `InstallationTarget` 包括15.0。
* 添加所需的安装必备组件（如以下示例中所示）。
  * 建议仅为安装先决条件指定组件 Id。
  * 请参阅本文档末尾的部分，了解有关[如何识别组件 id 的说明](#find-component-ids)。

示例：

```xml
<PackageManifest>
 ...
    <Prerequisites>
        <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Component.DiagnosticTools" Version="[15.0.25814.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Shell.12.0" Version="[12.0]" />
    </Prerequisites>
 ...
</PackageManifest>
```

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>选项：使用设计器对 VSIX 扩展清单进行更改

您可以使用清单设计器中的 "新建**必备项**" 选项卡来选择先决条件，将为您更新 XML，而不是直接编辑清单 XML。

> [!Note]
> 清单设计器将仅允许你选择在当前 Visual Studio 实例上安装的组件（而不是工作负荷或包）。 如果需要为当前未安装的工作负荷、包或组件添加必备组件，请直接编辑清单 XML。

* 打开*source.extension.vsixmanifest [Design]* 文件。
* 选择 "**系统必备**" 选项卡，然后按 "**新建**" 按钮。

   ![VSIX 清单设计器](media/vsix-manifest-designer.png)

* 将打开 "**添加新的先决条件**" 窗口。

   ![添加 vsix 必备组件](media/add-vsix-prerequisite.png)

* 单击 "**名称**" 的下拉列表，然后选择所需的必备组件。
* 如有必要，请更新版本。

   > [!Note]
   > "版本" 字段将使用当前已安装组件的版本进行预填充，范围是在组件的下一个主要版本中（但不包括）。

   ![添加 roslyn 必备组件](media/add-roslyn-prerequisite.png)

* 按“确定”。

## <a name="update-debug-settings-for-the-project"></a>更新项目的调试设置

如果要在 Visual Studio 的实验实例中调试扩展，请确保 "用于**调试**的项目设置" > "启动"**操作**具有设置为 Visual studio 2017 安装的*devenv*文件的 "**启动外部程序：** 值"。

它可能如下所示： *C:\Program Files （x86） \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe*

![启动外部程序](media/start-external-program.png)

> [!Note]
> 调试启动操作通常存储在 *.csproj*文件中。 此文件通常包含在 *.gitignore*文件中，因此，在提交到源代码管理时，通常不会将其保存到其他项目文件中。 同样，如果你已将解决方案从源代码管理中新提取，则项目可能不会为启动操作设置值。 使用 Visual Studio 2017 创建的新 VSIX 项目将使用创建的 *.csproj*文件，该文件使用指向当前 Visual studio 安装目录的默认值。 但是，如果要迁移 VSIX v2 扩展 *，则该文件可能*会包含对以前的 Visual Studio 版本的安装目录的引用。 当你尝试调试扩展时，将值设置为 "**调试** > **启动操作**" 将允许正确的 Visual Studio 实验实例启动。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>检查扩展是否已正确生成（作为 VSIX v3）

* 生成 VSIX 项目。
* 解压缩生成的 VSIX。
  * 默认情况下，VSIX 文件在*bin/Debug*或*bin/Release*内处于 *[YourCustomExtension] .vsix*内。
  * 将 *.vsix*重命名为 *.zip*即可轻松查看内容。
* 检查是否存在三个文件：
  * *extension.vsixmanifest*
  * *manifest.json*
  * *catalog.json*

## <a name="check-when-all-required-prerequisites-are-installed"></a>检查是否安装了所有必需的必备组件

测试是否已在安装了所有必需的必备组件的计算机上成功安装了 VSIX。

> [!Note]
> 在安装任何扩展之前，请关闭 Visual Studio 的所有实例。

尝试安装扩展：

* 在 Visual Studio 2017 上

![Visual Studio 2017 上的 VSIX 安装程序](media/vsixinstaller-vs-2017.png)

* 可选：检查以前版本的 Visual Studio。
  * 证明向后兼容性。
  * 适用于 Visual Studio 2012、Visual Studio 2013、Visual Studio 2015。
* 可选：检查 VSIX 安装程序版本检查器是否提供了版本选择。
  * 包括 Visual Studio 的早期版本（如果已安装）。
  * 包括 Visual Studio 2017。

如果最近打开了 Visual Studio，你可能会看到如下所示的对话框：

![vs 正在运行的进程](media/vs-running-processes.png)

等待进程关闭，或手动结束任务。 可以按列出的名称或括号中列出的 PID 查找进程。

> [!Note]
> 当 Visual Studio 的实例正在运行时，这些进程不会自动关闭。 请确保已在计算机上关闭 Visual Studio 的所有实例，包括其他用户的所有实例，然后继续重试。

## <a name="check-when-missing-the-required-prerequisites"></a>如果缺少所需的先决条件，请检查

* 尝试在使用 Visual Studio 2017 的计算机上安装扩展，该计算机不包含先决条件（以上）中定义的所有组件。
* 检查安装是否标识了缺少的组件，并在 VSIXInstaller 中将它们列出为必备组件。
* 注意：如果需要随扩展安装任何先决条件，则需要提升。

![vsixinstaller 缺少必备组件](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>确定组件

查找依赖项时，你会发现一个依赖项可能会映射到多个组件。 若要确定应将哪些依赖项指定为系统必备组件，建议选择一个组件，该组件的功能类似于你的扩展，并同时考虑你的用户以及他们最可能安装的组件类型不需要安装。 我们还建议以一种方式构建扩展，其中所需的先决条件仅满足仅允许运行扩展的最小值，并且如果未检测到某些组件，其他功能会使用户处于休眠状态。

为了提供进一步的指南，我们已确定了几种常见的扩展类型和其建议的先决条件：

Ą©展Ąą型 | 显示名称 | ID
--- | --- | ---
编辑器 | Visual Studio 核心编辑器 | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# 和 Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | 托管桌面工作负载核心 | Microsoft.VisualStudio.Component.ManagedDesktop.Core
调试器 | 实时调试器 | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>查找组件 Id

按 Visual Studio 产品排序的组件列表位于[Visual studio 2017 工作负荷和组件 id](/visualstudio/install/workload-and-component-ids?view=vs-2019)。 在清单中将这些组件 Id 用于必备 Id。

如果不确定哪个组件包含特定的二进制文件，请下载[组件 > 二进制映射电子表格](https://aka.ms/vs2017componentid-binaries)。

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-ComponentBinaryMapping.xlsx

Excel 工作表中有四列：**组件名称、组件名称**、**版本**和**二进制文件/文件名称**。  您可以使用筛选器搜索和查找特定组件和二进制文件。

对于所有引用，首先确定哪些是核心编辑器（VisualStudio. CoreEditor）组件中的引用。  至少需要将核心编辑器组件指定为所有扩展的必备组件。 对于不在核心编辑器中的引用，请在 "**二进制文件/文件名称**" 部分中添加筛选器，以查找具有这些引用的任意子集的组件。

例如：

* 如果你有一个调试器扩展，并且知道你的项目具有对*vsdebugeng.dll*和*VSDebug*的引用，请在 "**二进制文件/文件名称**" 标头中单击 "筛选器" 按钮。  搜索 "Vsdebugeng.dll"，然后选择 *"确定*"。  接下来，再次单击 "**二进制文件名称**" 标头中的 "筛选器" 按钮，然后搜索 "VSDebug"。  选中 "**添加当前所选内容**" 复选框，然后选择 **"确定"** 。  现在，浏览**组件名称**，查找与扩展类型最相关的组件。 在此示例中，你将选择实时调试器并将其添加到你的 source.extension.vsixmanifest。
* 如果你知道你的项目处理调试器元素，则可以在筛选器搜索框中搜索 "调试器"，以查看其名称中包含调试器的组件。

## <a name="specify-a-visual-studio-2017-release"></a>指定 Visual Studio 2017 版本

例如，如果你的扩展需要特定版本的 Visual Studio 2017 （例如，它依赖于15.3 中发布的功能），则必须在 VSIX **InstallationTarget**中指定内部版本号。 例如，版本15.3 的生成号为 "15.0.26730.3"。 可在[此处](../install/visual-studio-build-numbers-and-release-dates.md)查看生成编号的版本映射。 使用版本号 "15.3" 将不能正常工作。

如果扩展需要15.3 或更高版本，则需要将**InstallationTarget 版本**声明为 [15.0.26730.3，16.0）：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```
