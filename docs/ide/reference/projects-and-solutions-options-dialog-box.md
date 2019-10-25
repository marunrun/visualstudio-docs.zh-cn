---
title: “选项”对话框 >“项目和解决方案”
ms.date: 07/26/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.General
helpviewer_keywords:
- Projects and Solutions Options dialog box
- Options dialog box, Projects and Solutions
ms.assetid: 2801f24e-a138-488a-ae3c-e1f99a678ac0
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 783cdf5cef127a39958f14a2dc5ece9a45fcee62
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655725"
---
# <a name="options-dialog-box-projects-and-solutions--general"></a>“选项”对话框：“项目和解决方案”\>“常规”

使用此页可定义与项目和解决方案相关的 Visual Studio 行为。 要访问这些选项，请选择“工具” > “选项”，展开“项目和解决方案”，再选择“常规”     。

“常规”页上提供了下列选项  。

## <a name="always-show-error-list-if-build-finishes-with-errors"></a>如果生成完成时有错误，则始终显示错误列表

仅当项目无法生成时，在完成生成时将打开“错误列表”  窗口。 将显示在生成过程中发生的错误。 如果清除此选项，则仍将发生错误，但在完成生成时窗口将不会打开。 默认情况下会启用此选项。

## <a name="track-active-item-in-solution-explorer"></a>跟踪解决方案资源管理器中的活动项

当选中时，“解决方案资源管理器”  将自动打开，活动项处于选中状态。 选定的项根据您在项目或解决方案中使用的不同文件或设计器中的不同组件而不同。 清除此选项后，“解决方案资源管理器”  中的所选内容不会自动更改。 默认情况下会启用此选项。

## <a name="show-advanced-build-configurations"></a>显示高级生成配置

当选中时，生成配置选项显示在“项目属性页”  对话框和“解决方案属性页”  对话框中。 如果未选中，对于包含一个配置或两个配置调试和发布的 Visual Basic 和 C# 项目，生成配置选项将不显示在“项目属性页”对话框和“解决方案属性页”对话框中   。 如果一个项目具有用户定义的配置，则会显示生成的配置选项。

未选中时，“生成”  菜单上的命令（如“生成解决方案”  、“重新生成解决方案”  和“清理解决方案”  ）将在发布配置上执行，“调试”  菜单上的命令（如“启动调试”  和“启动但不调试”  ）将在调试配置上执行。

## <a name="always-show-solution"></a>总是显示解决方案

如果选中，该解决方案和解决方案中执行的所有命令将始终显示在 IDE 中。 未选中时，如果该解决方案只包含一个项目，所有项目将作为独立项目创建，您不会看到在解决方案资源管理器中的解决方案或 IDE 中解决方案的执行命令。

::: moniker range="vs-2017"

## <a name="save-new-projects-when-created"></a>创建时保存新项目

当选中时，你可以在“新建项目”  对话框中为你的项目指定位置。 如果未选中，所有新项目将创建为临时项目。 当您正在使用临时项目时，您可以创建和试验项目，无需指定磁盘位置。

::: moniker-end

## <a name="warn-user-when-the-project-location-is-not-trusted"></a>当项目位置不受信任时警告用户

如果您尝试在不完全信任的位置（例如，在 UNC 路径或 HTTP 路径）创建一个新项目或打开现有项目，将显示一条消息。 使用此选项以指定每次在不完全受信任的位置尝试创建或打开一个项目时是否显示该消息。

## <a name="show-output-window-when-build-starts"></a>在生成开始时显示输出窗口

在解决方案生成一开始就在 IDE 中自动显示[输出窗口](../../ide/reference/output-window.md)。

## <a name="prompt-for-symbolic-renaming-when-renaming-files"></a>在重命名文件时提示重命名符号

选定后，Visual Studio 将显示一个消息框，询问是否还应该将项目中的所有引用重命名为代码元素。

## <a name="prompt-before-moving-files-to-a-new-location"></a>将文件移动到新位置之前显示提示

选定后，在通过解决方案资源管理器中的操作更改文件的位置之前，Visual Studio 会显示确认消息框  。

## <a name="reopen-documents-on-solution-load"></a>加载解决方案时重新打开文档

选中后，此解决方案上次关闭时打开的文档将在解决方案打开时自动打开。

重新打开某些类型的文件或设计器会延迟解决方案加载。 如果不想还原解决方案的上一个上下文，请取消选中此选项以[提高解决方案加载性能](../../ide/visual-studio-performance-tips-and-tricks.md#disable-automatic-file-restore)。

::: moniker range=">=vs-2019"

## <a name="restore-solution-explorer-project-hierarchy-state-on-solution-load"></a>加载解决方案时还原解决方案资源管理器项目层次结构状态

选择该选项后，将根据解决方案上次打开时是否展开或折叠节点，还原解决方案资源管理器中的节点状态。 取消选择此选项可缩短大型解决方案的解决方案加载时间。

> [!TIP]
> 如果禁用此选项，要导航到解决方案资源管理器中的活动文档，一种简单的方法就是在“解决方案资源管理器”工具栏上选择“与活动文档同步”   。
>
> ![与解决方案资源管理器中的活动文档同步](media/sync-active-document.png)

## <a name="open-sdk-style-project-files-with-double-click-or-the-enter-key"></a>通过双击或按 Enter 打开 SDK 样式项目文件

选择此选项后，双击解决方案资源管理器中的 SDK 样式项目节点或选择它，然后按 Enter，项目文件（例如 .csproj 文件）将在编辑器中以 XML 格式打开  \*。 取消选择后，在解决方案资源管理器中双击 SDK 样式的项目节点或选择它并按 Enter 只可展开或折叠节点  。

如果未选择此选项并且要编辑 SDK 样式的项目文件，请在解决方案资源管理器中右键单击项目节点，然后选择“编辑项目文件”  。 对于其他项目类型，必须先卸载项目，然后才能在 Visual Studio 中进行编辑。

> [!TIP]
> SDK 样式的项目或[项目 SDK](../../msbuild/how-to-use-project-sdk.md) 具有较新的、更精简的项目文件格式，该格式已在 MSBuild 15.0 中引入  。 SDK 样式的项目在 `Project` 元素上包含 `Sdk` 属性，例如 `<Project Sdk="Microsoft.NET.Sdk">`。 例如，从 Visual Studio 模板之一创建一个新的 .NET Core 项目时，Visual Studio 将创建一个 SDK 样式的项目。

::: moniker-end

## <a name="see-also"></a>请参阅

- [“选项”对话框：“项目和解决方案”\>“位置”](projects-solutions-locations-options.md)
- [“选项”对话框 ->“项目和解决方案”->“生成和运行”](../../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [“选项”对话框 ->“项目和解决方案”->“Web 项目”](../../ide/reference/options-dialog-box-projects-and-solutions-web-projects.md)
