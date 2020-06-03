---
title: 管理项目中的引用
ms.date: 08/02/2019
ms.topic: conceptual
f1_keywords:
- vs.ProjectPropertiesReferencePaths
- cs.ProjectPropertiesReferencePaths
helpviewer_keywords:
- C# projects, references
- referencing objects, project references
- external component references
- referencing namespaces
- Visual Basic projects, references
- referencing components, external components
- Web references, types of project references
- namespaces [Visual Studio], referencing
- COM components, referencing
- objects [Visual Studio], referencing
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c55b0d3487eb18db33805b418882f157d55b1253
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183530"
---
# <a name="manage-references-in-a-project"></a>管理项目中的引用

在对外部组件或连接的服务编写代码之前，你的项目必须首先包含对它的引用。 引用实质上是项目文件中包含 Visual Studio 定位组件或服务所需信息的条目。

若要添加引用，请右键单击“解决方案资源管理器”中的“引用”或“依赖项”节点，然后选择“添加引用”   。 还可以右键单击项目节点，然后选择“添加” > “引用” 。 有关详细信息，请参阅[如何：添加或删除引用](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)。

![在 Visual C&#43;&#43; 中添加引用](../ide/media/vs2015_cpp_add_reference.png)

可对以下类型的组件和服务添加引用：

- .NET 类库或程序集

- UWP 应用

- COM 组件

- 同一解决方案中项目的其他程序集或类库

- 共享项目

- XML Web services

## <a name="uwp-app-references"></a>UWP 应用的引用

### <a name="project-references"></a>项目引用

通用 Windows 平台 (UWP) 项目可以创建对解决方案中其他 UWP 项目的引用，也可以创建对 Windows 8.1 项目或二进制文件的引用，前提是这些项目不使用 Windows 10 中已弃用的 API。 有关详细信息，请参阅 [从 Windows Runtime 8 移动到 UWP](/windows/uwp/porting/w8x-to-uwp-root)。

如果选择将 Windows 8.1 项目重定向到 Windows 10，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)。

### <a name="extension-sdk-references"></a>扩展 SDK 引用

Visual Basic、C#、C++ 和 JavaScript 通用 Windows 平台 (UWP) 应用可以引用面向 Windows 8.1 的扩展 SDK，前提是这些扩展 SDK 不使用 Windows 10 中已弃用的 API。 请查看扩展 SDK 供应商站点，确定它是否可由 UWP 应用引用。

如果确定你的应用所引用的扩展 SDK 不受支持，则需执行以下步骤：

1. 查看导致错误的项目的名称。 项目所面向的平台记录在项目名称旁的括号中。 例如，“MyProjectName (Windows 8.1)”  表示项目 MyProjectName 面向平台版本 Windows 8.1。

1. 转到拥有不受支持的扩展 SDK 的供应商站点，安装具有与你的项目所面向的平台版本兼容的依赖项的扩展 SDK 版本。

    > [!NOTE]
    > 查看“引用管理器”是一种了解某扩展 SDK 是否在其他扩展 SDK 上具有依赖关系的方法。 重启 Visual Studio，创建新的 C# UWP 应用项目，然后右键单击该项目并选择“添加引用”。 依次转到“Windows”选项卡、“扩展”子选项卡，选择该扩展 SDK。 查看“引用管理器”中的右窗格。 如果具有依赖关系，则将在该位置列出依赖关系。

    > [!IMPORTANT]
    > 如果项目面向 Windows 10，并且上一步中安装的扩展 SDK 在 Microsoft Visual C 运行时包上具有依赖关系，则与 Windows 10 兼容的 Microsoft Visual C++ 运行时包的版本为 v14.0，并与 Visual Studio 一起安装。

1. 如果上一步中安装的扩展 SDK 在其他扩展 SDK 上具有依赖关系，请转到拥有依赖关系的供应商站点，并安装与项目所面向的平台版本相兼容的版本的依赖项。

1. 重启 Visual Studio 并打开你的应用。

1. 右键单击项目中导致错误的“引用”或“依赖项”节点，然后选择“添加引用”  。

1. 依次单击“Windows”选项卡、“扩展”子选项卡，然后取消勾选旧扩展 SDK 的复选框，并勾选新扩展 SDK 的复选框。 单击 **“确定”** 。

## <a name="add-a-reference-at-design-time"></a>在设计时添加引用

对项目中的程序集进行引用时，Visual Studio 在以下位置搜索程序集：

- 当前项目目录。 （可以使用 **“浏览”** 选项卡查找这些程序集。）

- 同一解决方案中的其他项目目录。 （可以在 **“项目”** 选项卡上找到这些程序集。）

> [!NOTE]
> - 所有项目均包含对 mscorlib 的隐式引用。
> - 所有项目都包含对 `System.Core` 的隐式引用，即使从引用列表中移除了 `System.Core` 也是如此。
> - Visual Basic 项目包含对 <xref:Microsoft.VisualBasic>的隐式引用。

## <a name="references-to-shared-components-at-run-time"></a>在运行时对共享组件的引用

在运行时，组件必须位于项目的输出路径或 Global Assembly Cache (GAC) 中。 如果项目中包含对某个对象的引用，但该对象不是上述的其中一个位置，则必须在生成项目时将该引用复制到项目的输出路径。 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 属性指示是否必须进行复制。 如果值为 **True**，则生成项目时，引用将复制到项目目录。 如果值为 **False**，则不复制引用。

如果你部署的应用程序中包含对 GAC 中注册的自定义组件的引用，则无论采用何种 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 设置，组件都不会随应用程序一起部署。 在 Visual Studio 的早期版本中，可以在引用上设置 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 属性，确保程序集已部署。 现在，必须手动将程序集添加到 \Bin 文件夹。 这会对所有自定义代码进行详细审查，以降低你发布不熟悉的自定义代码的风险。

默认情况下，如果程序集或组件位于全局程序集缓存中或者是框架组件，则 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 属性设置为 **False** 。 否则，值设置为 **True**。 项目到项目的引用始终设置为 **True**。

## <a name="reference-a-project-or-assembly-that-targets-a-different-version-of-net"></a>引用面向不同 .NET 版本的项目或程序集

可以创建一些应用程序，这些应用程序引用的项目或程序集面向 .NET 的不同版本。 例如，可以创建一个面向 .NET Framework 4.6 的应用程序，该应用程序引用面向 .NET Framework 4.5 的程序集。 如果创建的项目面向 .NET 的早期版本，则无法在该项目中设置对面向更新版本的项目或程序集的引用。

有关详细信息，请参阅[框架定位概述](../ide/visual-studio-multi-targeting-overview.md)。

## <a name="project-to-project-references"></a>项目到项目的引用

项目到项目的引用是对包含程序集的项目的引用；通过使用“引用管理器”对话框中的“项目”选项卡添加项目引用。 给定项目路径后，Visual Studio 可以找到程序集。

如果拥有生成程序集的项目，则应引用该项目并且不使用文件引用（见下文）。 项目到项目的引用的一个优点是能够在生成系统中的项目之间创建依赖关系。 如果依赖项目在上次生成引用项目之后已发生更改，则将生成该依赖项目。 文件引用不会创建生成依赖关系，因此可以在不生成依赖项目的情况下生成引用项目，并且该引用可能会过时。 （也就是说，项目可以引用以前生成的项目版本。）这可能导致 bin 目录中所需的单个 DLL 同时存在多个版本，而这种情况实际是不可能出现的。 当此冲突发生时，你将看到一条消息，例如“警告：无法将项目 ‘project’ 中的依赖关系‘file’复制到运行目录，因为它将覆盖引用 ‘file’。”。 有关详细信息，请参阅[有关无效引用的疑难解答](../ide/troubleshooting-broken-references.md)和[如何：创建和删除项目依赖项](../ide/how-to-create-and-remove-project-dependencies.md)。

> [!NOTE]
> 如果一个项目的目标 .NET Framework 版本是 4.5，而另一个项目的目标版本是 2、3、3.5 或 4.0，则创建的是文件引用而非项目到项目的引用。

## <a name="shared-project-references"></a>共享项目引用

与大多数其他项目类型不同，共享项目不包含任何二进制文件输出。 相反，代码将编译到引用它的每个项目中。 使用[共享项目](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)，可以编写由多个不同的应用程序项目引用的通用代码。 此代码作为每个引用项目的一部分进行编译，并且可以包含编译器指令以帮助将特定于平台的功能合并到共享代码库中。 在“引用管理器”对话框的“共享项目”选项卡上添加对共享项目的引用。

## <a name="file-references"></a>文件引用

文件引用是对 Visual Studio 项目上下文之外的程序集的直接引用。 通过使用“引用管理器”对话框中的“浏览”选项卡进行创建。 当只有程序集或组件，而没有将其创建为输出的项目时，使用文件引用。

## <a name="see-also"></a>请参阅

- [有关损坏的引用的疑难解答](../ide/troubleshooting-broken-references.md)
- [如何：添加或删除引用](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)
