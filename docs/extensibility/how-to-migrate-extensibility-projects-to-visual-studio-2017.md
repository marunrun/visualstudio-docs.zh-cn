---
title: 如何：将扩展性项目迁移到视觉工作室 2017 |微软文档
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: b0cae0261b185ee08400e5f3d25735634663f54a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710983"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>如何：将扩展性项目迁移到 Visual Studio 2017

本文档介绍如何将扩展性项目升级到 Visual Studio 2017。 除了描述如何更新项目文件外，它还介绍了如何从扩展清单版本 2 （VSIX v2） 升级到新版本 3 VSIX 清单格式 （VSIX v3）。

## <a name="install-visual-studio-2017-with-required-workloads"></a>安装带有所需工作负载的可视化工作室 2017

确保您的安装包括以下工作负载：

* .NET 桌面开发
* Visual Studio 扩展开发

## <a name="open-vsix-solution-in-visual-studio-2017"></a>2017年在视觉工作室开放 VSIX 解决方案

所有 VSIX 项目都需要将主要版本单向升级到 Visual Studio 2017。

项目文件（例如 =*.csproj）* 将更新：

* 最小视觉工作室版本 - 现在设置为 15.0
* 旧工具版本（如果以前存在） - 现在设置为 14.0

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>更新 Microsoft.VSSDK.BuildTools NuGet 包

> [!Note]
> 如果您的解决方案不引用 Microsoft.VSSDK.BuildTools NuGet 包，您可以跳过此步骤。

为了以新的 VSIX v3（版本 3）格式构建扩展，需要使用新的 VSSDK 构建工具构建解决方案。 这将与 Visual Studio 2017 一起安装，但您的 VSIX v2 扩展可能通过 NuGet 保留对旧版本的引用。 如果是这样，您需要手动安装 Microsoft.VSSDK.BuildTools NuGet 包的更新。

要更新对 Microsoft.VSSDK.BuildTools 的 NuGet 引用，

* 右键单击解决方案，然后选择 **"管理 NuGet 包以用于解决方案**"。
* 导航到 **"更新**"选项卡。
* 选择**微软.VSSDK.BuildTools（最新版本）**.
* 按**更新**。

![VSSDK 构建工具](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>更改 VSIX 扩展清单

为了确保用户安装 Visual Studio 具有运行扩展所需的所有程序集，请在扩展清单文件中指定所有先决条件组件或包。 当用户尝试安装扩展时，VSIX安装程序将检查是否安装了所有先决条件。 如果缺少某些组件，系统将提示用户安装缺少的组件，作为扩展安装过程的一部分。

> [!Note]
> 至少，所有扩展都应指定 Visual Studio 核心编辑器组件作为先决条件。

* 编辑扩展名清单文件（通常称为*source.扩展.vsixmanifest）。*
* 确保`InstallationTarget`包含 15.0。
* 添加所需的安装先决条件（如下例所示）。
  * 我们建议您仅为安装先决条件指定组件指示。
  * 有关[识别组件标识](#find-component-ids)的说明，请参阅本文档末尾的部分。

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

您可以使用清单设计器中的新**先决条件**选项卡来选择先决条件，并将为您更新 XML，而不是直接编辑清单 XML。

> [!Note]
> 清单设计器仅允许您选择当前 Visual Studio 实例上安装的组件（不是工作负载或包）。 如果需要为当前未安装的工作负荷、包或组件添加先决条件，请直接编辑清单 XML。

* *开源.扩展.vsixmanifest [设计]* 文件。
* 选择 **"先决条件"** 选项卡，然后按 **"新建"** 按钮。

   ![VSIX 清单设计器](media/vsix-manifest-designer.png)

* 将打开"**添加新先决条件"** 窗口。

   ![添加 v6 先决条件](media/add-vsix-prerequisite.png)

* 单击 **"名称"** 的下拉列表并选择所需的先决条件。
* 如有必要，请更新版本。

   > [!Note]
   > 版本字段将预填充当前安装的组件的版本，其范围范围将不超过（但不包括）组件的下一个主要版本。

   ![添加罗斯林先决条件](media/add-roslyn-prerequisite.png)

* 按 **“确定”**。

## <a name="update-debug-settings-for-the-project"></a>更新项目的调试设置

如果要在 Visual Studio 的实验实例中调试扩展，请确保**调试** > **开始操作**的项目设置具有 **"开始"外部程序：** 值设置为 Visual Studio 2017 安装的*devenv.exe*文件。

它可能看起来像： *C：_程序文件 （x86）\微软可视化工作室\2017_企业_Common7_IDE_devenv.exe*

![启动外部程序](media/start-external-program.png)

> [!Note]
> 调试启动操作通常存储在 *.csproj.user*文件中。 此文件通常包含在 *.gitignore*文件中，因此，当提交到源代码管理时，通常不会与其他项目文件一起保存。 因此，如果您刚刚从源代码管理中拉出解决方案，则项目很可能没有为"开始操作"设置任何值。 使用 Visual Studio 2017 创建的新 VSIX 项目将创建一个 *.csproj.user*文件，默认指向当前 Visual Studio 安装目录。 但是，如果要迁移 VSIX v2 扩展名，*则 .csproj.user*文件可能包含对以前 Visual Studio 版本的安装目录的引用。 设置**调试** > **启动操作**的值将允许在尝试调试扩展时启动正确的 Visual Studio 实验实例。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>检查扩展是否正确生成（作为 VSIX v3）

* 构建 VSIX 项目。
* 解压缩生成的 VSIX。
  * 默认情况下，VSIX 文件位于*bin/调试*或*bin/释放*中，作为 *[您的自定义扩展]vsix*。
  * 将 *.vsix*重命名为 *.zip，* 以便轻松查看内容。
* 检查是否存在三个文件：
  * *扩展.vsix清单*
  * *清单.json*
  * *目录.json*

## <a name="check-when-all-required-prerequisites-are-installed"></a>检查何时安装了所有必需的先决条件

测试 VSIX 是否成功安装在安装了所有必需先决条件的计算机上。

> [!Note]
> 在安装任何扩展之前，请关闭 Visual Studio 的所有实例。

尝试安装扩展：

* 在视觉工作室 2017

![Visual Studio 2017 上的 VSIX 安装程序](media/vsixinstaller-vs-2017.png)

* 可选：检查早期版本的可视化工作室。
  * 证明向后兼容性。
  * 应适用于 Visual Studio 2012， 视觉工作室 2013， 视觉工作室 2015.
* 可选：检查 VSIX 安装程序版本检查器提供版本选择。
  * 包括早期版本的可视化工作室（如果已安装）。
  * 包括视觉工作室 2017.

如果最近打开了 Visual Studio，您可能会看到如下所示的对话框：

![与正在运行的进程](media/vs-running-processes.png)

等待进程关闭或手动结束任务。 您可以按列出的名称查找进程，也可以在括号中列出 PID。

> [!Note]
> 在运行 Visual Studio 实例时，这些进程不会自动关闭。 确保已关闭计算机上的所有 Visual Studio 实例，包括其他用户的实例，然后继续重试。

## <a name="check-when-missing-the-required-prerequisites"></a>检查何时缺少所需的先决条件

* 尝试在具有 Visual Studio 2017 的计算机上安装扩展，该计算机不包含先决条件中定义的所有组件（上图）。
* 检查安装标识缺少的组件，并将其列为 VSIX 安装程序的先决条件。
* 注意：如果需要随扩展一起安装任何先决条件，则需要提升。

![vsix安装程序缺少先决条件](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>决定组件

查找依赖项时，您会发现一个依赖项可以映射到多个组件。 为了确定应指定哪些依赖项作为先决条件，我们建议您选择具有与扩展类似的功能的组件，并考虑您的用户以及他们最有可能安装或不介意安装的组件类型。 我们还建议构建扩展，使所需的先决条件仅满足允许扩展运行的最小值，并且如果没有检测到某些组件，则其他功能的扩展将处于休眠状态。

为了提供进一步的指导，我们确定了一些常见的扩展类型及其建议的先决条件：

扩展类型 | 显示名称 | ID
--- | --- | ---
编辑器 | Visual Studio 核心编辑器 | Microsoft.VisualStudio.Component.CoreEditor
罗斯林 | C# 和 Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | 托管桌面工作负载核心 | Microsoft.VisualStudio.Component.ManagedDesktop.Core
调试程序 | 实时调试器 | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>查找组件指示

Visual Studio 产品排序的组件列表位于[Visual Studio 2017 工作负载和组件 IT。](/visualstudio/install/workload-and-component-ids?view=vs-2019) 将这些组件的代号用于清单中的先决条件。

如果您不确定哪个组件包含特定的二进制文件，请下载组件[-> 二进制映射电子表格](https://aka.ms/vs2017componentid-binaries)。

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-组件二进制映射.xlsx

Excel 工作表中有四列：**组件名称**、组件**Id、****版本**和**二进制/文件名**。  您可以使用筛选器来搜索和查找特定的组件和二进制文件。

对于所有引用，请先确定哪些引用位于核心编辑器（Microsoft.VisualStudio.组件.核心编辑器）组件中。  至少，我们需要将核心编辑器组件指定为所有扩展的先决条件。 在不在核心编辑器中留下的引用中，在 **"二进制/文件名称**"部分中添加筛选器，以查找具有这些引用任何子集的组件。

示例：

* 如果您有调试器扩展名，并且知道项目具有*VSDebugEng.dll*和*VSDebug.dll*的引用，请单击 **"二进制/文件名称**"标题中的筛选器按钮。  搜索"VSDebugEng.dll"并选择 *"确定*"。  接下来，再次单击 **"二进制/文件名称**"标题中的筛选器按钮，然后搜索"VSDebug.dll"。  选择复选框 **"添加当前选择以筛选**"并选择 **"确定**"。  现在浏览**组件名称**，查找与您的扩展类型最相关的组件。 在此示例中，您将选择"准时调试器"并将其添加到 vsixmanifest 中。
* 如果您知道项目涉及调试器元素，则可以在筛选器搜索框中搜索"调试器"以查看哪些组件在其名称中包含调试器。

## <a name="specify-a-visual-studio-2017-release"></a>指定视觉工作室 2017 版本

例如，如果扩展需要 Visual Studio 2017 的特定版本，则它取决于 15.3 中发布的功能，则必须在 VSIX**安装目标**中指定内部版本号。 例如，版本 15.3 的生成号为"15.0.26730.3"。 你可以[在这里](../install/visual-studio-build-numbers-and-release-dates.md)看到版本映射以生成数字。 使用版本号"15.3"将不能正常工作。

如果您的扩展需要 15.3 或更高版本，您将声明**安装目标版本**为 [15.0.26730.3， 16.0）：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```
