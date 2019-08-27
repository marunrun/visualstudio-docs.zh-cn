---
title: 如何往返扩展
ms.date: 06/25/2017
ms.topic: conceptual
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: madsk
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: 392a0157522f5baa8e8736d52c940b31c0a44cde
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67826033"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-2017-and-visual-studio-2015"></a>如何：使扩展与 Visual Studio 2017 和 Visual Studio 2015 兼容

本文档介绍如何使 Visual Studio 2015 和 Visual Studio 2017 之间往返扩展性项目。 完成此升级之后，将能够打开、 生成、 安装和运行 Visual Studio 2015 和 Visual Studio 2017 中一个项目。 作为参考，可以中找到一些扩展，可以 Visual Studio 2015 和 Visual Studio 2017 之间的往返[VS SDK 扩展性示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

如果只想生成在 Visual Studio 2017 中，但却希望输出 VSIX，若要在 Visual Studio 2015 和 Visual Studio 2017 中运行，请参阅[扩展迁移文档](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

> [!NOTE]
> 由于在 Visual Studio 版本之间的更改，在另一个，都在一个版本中工作的一些事项不起作用。 请确保这两个版本中提供了你尝试访问的功能或扩展都将有意外的结果。

下面是将完成保存/还原 VSIX 本文档中的步骤概述：

1. 导入正确的 NuGet 包。
2. 更新扩展清单：
    * 安装目标
    * 系统必备
3. 更新 CSProj:
    * 更新`<MinimumVisualStudioVersion>`。
    * 添加`<VsixType>`属性。
    * 添加调试属性`($DevEnvDir)`3 次。
    * 添加用于导入生成的工具和目标的条件。

4. 生成和测试

## <a name="environment-setup"></a>环境设置

此文档假设已在计算机上安装以下组件：

* 安装了 VS sdk 的 visual Studio 2015
* 安装了扩展工作负载的 visual Studio 2017

## <a name="recommended-approach"></a>建议的方法

强烈建议使用 Visual Studio 2015 中，而不是 Visual Studio 2017 中启动此升级。 在 Visual Studio 2015 中开发的主要优势是为了确保不引用在 Visual Studio 2015 中不可用的程序集。 如果进行 Visual Studio 2017 中的开发，则可能会引入对 Visual Studio 2017 中仅存在于程序集依赖项的风险。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>确保没有对 project.json 引用

我们将在本文档后面插入条件导入语句中的为你 * *.csproj*文件。 如果 NuGet 引用存储在中，这不起作用*project.json*。 在这种情况下，因此建议将移动到的所有 NuGet 引用*packages.config*文件。
如果您的项目包含*project.json*文件：

* 记下中的引用*project.json*。
* 从**解决方案资源管理器**，删除*project.json*从项目文件。 这会删除*project.json*文件，并将其从项目删除。
* 添加 NuGet 引用中返回到项目：
  * 右键单击**解决方案**，然后选择**为解决方案管理 NuGet 包**。
  * Visual Studio 自动创建*packages.config*为你的文件。

> [!NOTE]
> 如果你的项目包含 EnvDTE 包，它们可能需要通过右键单击要添加**引用**选择**添加引用**并添加适当的引用。 使用 NuGet 包可能会尝试生成项目时创建的错误。

## <a name="add-appropriate-build-tools"></a>添加相应的生成工具

我们确保需要添加将使我们能够生成和调试适当的生成工具。 Microsoft 已创建此调用 Microsoft.VisualStudio.Sdk.BuildTasks 程序集。

若要生成并部署在 Visual Studio 2015 和 2017 VSIXv3，将需要以下 NuGet 包：

Version | 生成的工具
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2017 | Microsoft.VSSDK.BuildTool

为此，请执行以下操作：

* 向项目添加 NuGet 包 Microsoft.VisualStudio.Sdk.BuildTasks.14.0。
* 如果你的项目不包含 Microsoft.VSSDK.BuildTools，请将其添加。
* 确保 15.x Microsoft.VSSDK.BuildTools 版本或更高版本。

## <a name="update-extension-manifest"></a>更新扩展清单

### <a name="1-installation-targets"></a>1.安装目标

我们需要告知目标进行生成 VSIX 何种版本的 Visual Studio。 通常情况下，这些引用是到版本 14.0 (Visual Studio 2015)、 版本 15.0 (Visual Studio 2017) 或版本 16.0 (Visual Studio 2019)。 在本例中，我们想要生成的 VSIX 将安装扩展的同时，因此，我们需要以这两个版本为目标。 如果你想在 VSIX 生成并安装在版本早于 14.0，这可以通过设置的更早的版本号;但是，不再支持版本 10.0 及更早版本。

* 打开*source.extension.vsixmanifest* Visual Studio 中的文件。
* 打开**安装目标**选项卡。
* 更改**版本范围**到 [14.0，17.0）。 [会告知 Visual Studio 包括过去它 14.0 和所有版本。 ')' 会告知 Visual Studio 包含所有版本，但不是包括，版本 17.0。
* 保存所有更改并关闭 Visual Studio 的所有实例。

![安装目标映像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2.添加到的先决条件*extension.vsixmanifest*文件

作为先决条件，我们需要 Visual Studio 核心编辑器。 打开 Visual Studio 并更新清单设计器用于插入了系统必备组件。

若要手动此操作：

* 导航到在文件资源管理器中的项目目录。
* 打开*extension.vsixmanifest*使用文本编辑器的文件。
* 添加以下标记：

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* 保存并关闭文件。

> [!NOTE]
> 您可能需要手动编辑系统必备组件的版本，以确保它是与所有版本的 Visual Studio 2017 兼容。 这是因为在设计器将插入的最低版本为当前版本的 Visual Studio (例如，15.0.26208.0)。 但是，由于其他用户可能具有较早版本，因此将需要手动编辑此字段为 15.0。

此时，你的清单文件应如下所示：

![先决条件示例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>修改项目文件 (myproject.csproj)

强烈建议以具有对已修改.csproj 打开时执行此步骤的引用。 您可以找到几个示例[此处](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。 选择任何可扩展性示例中，找到 *.csproj*文件的引用，并执行以下步骤：

* 导航到在项目目录**文件资源管理器**。
* 打开*myproject.csproj*使用文本编辑器的文件。

### <a name="1-update-the-minimumvisualstudioversion"></a>1.更新 MinimumVisualStudioVersion

* 将最小的 visual studio 版本设置为`$(VisualStudioVersion)`和为其添加条件语句。 如果不存在，请添加这些标记。 请确保按如下所示设置标记：

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2.添加 VsixType 属性。

* 添加以下标记`<VsixType>v3</VsixType>`到属性组。

> [!NOTE]
> 建议将此添加下面`<OutputType></OutputType>`标记。

### <a name="3-add-the-debugging-properties"></a>3.添加的调试属性

* 添加以下属性组：

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartPrograms>$(DevEnvDir)devenv.exe</StartPrograms>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* 删除从下面的代码示例的所有实例 *.csproj*文件和任何 *。 csproj.user*文件：

```xml
<StartAction>Program</StartAction>
<StartPrograms>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartPrograms>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4.将条件添加到生成工具导入

* 添加到其他条件语句`<import>`Microsoft.VSSDK.BuildTools 引用的标记。 插入`'$(VisualStudioVersion)' != '14.0' And`前面的条件语句。 这些语句将出现在页眉和页脚的 csproj 文件。

例如:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* 添加到其他条件语句`<import>`具有 Microsoft.VisualStudio.Sdk.BuildTasks.14.0 的标记。 插入`'$(VisualStudioVersion)' == '14.0' And`前面的条件语句。 这些语句将出现在页眉和页脚的 csproj 文件。

例如：

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* 添加到其他条件语句`<Error>`Microsoft.VSSDK.BuildTools 引用的标记。 执行此操作的方法是插入`'$(VisualStudioVersion)' != '14.0' And`前面的条件语句。 这些语句将出现在 csproj 文件的页脚。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* 添加到其他条件语句`<Error>`具有 Microsoft.VisualStudio.Sdk.BuildTasks.14.0 的标记。 插入`'$(VisualStudioVersion)' == '14.0' And`前面的条件语句。 这些语句将出现在 csproj 文件的页脚。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* 保存 csproj 文件并将其关闭。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2017"></a>Visual Studio 2015 和 Visual Studio 2017 中的测试扩展安装

此时，你的项目应准备好生成可以在 Visual Studio 2015 和 Visual Studio 2017 安装 VSIXv3。

* 在 Visual Studio 2015 中打开你的项目。
* 生成项目并确认输出是否正确生成 VSIX 中。
* 导航到你的项目目录。
* 打开 *\bin\Debug* 文件夹。
* 双击 VSIX 文件，并在 Visual Studio 2015 和 Visual Studio 2017 上安装您的扩展插件。
* 请确保你可以查看扩展的**工具** > **扩展和更新**中**已安装**部分。
* 尝试运行/使用要检查其运行的扩展。

![查找 VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> 如果你的项目并显示消息挂起**打开的文件**，强制关闭 Visual Studio、 导航到你的项目目录、 显示隐藏的文件夹，并删除 *.vs*文件夹。
