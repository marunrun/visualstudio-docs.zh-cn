---
title: 管理项目中的引用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ProjectPropertiesReferencePaths
- cs.ProjectPropertiesReferencePaths
helpviewer_keywords:
- Visual C# projects, references
- referencing objects, project references
- external component references
- referencing namespaces
- Visual Basic projects, references
- referencing components, external components
- Web references, types of project references
- namespaces [Visual Studio], referencing
- COM components, referencing
- objects [Visual Studio], referencing
ms.assetid: 05d1c51b-44f3-4973-8a11-6c919b08ad62
caps.latest.revision: 55
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1f2f3c26d89616f083c218c6b11610fe5e329a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651319"
---
# <a name="managing-references-in-a-project"></a>管理项目中的引用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在对外部组件或连接的服务编写代码之前，你的项目必须首先包含对它的引用。 引用实质上是项目文件中包含 Visual Studio 定位组件或服务所需信息的条目。

 若要添加引用，请右键单击“解决方案资源管理器”中的“引用”节点，然后选择 **“添加引用”**。 有关详细信息，请参阅 [How to: Add or Remove References By Using the Reference Manager](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)。

 ![在 Visual C&#43;&#43; 中添加引用](../ide/media/vs2015-cpp-add-reference.png "vs2015_cpp_add_reference")

 可以对以下类型的组件/服务设置引用：

- Windows 应用商店应用的引用

- .NET framework 类库或程序集

- COM 组件

- 同一解决方案中项目的其他程序集或类库

- XML Web services

## <a name="windows-store-app-references"></a>Windows 应用商店应用的引用

### <a name="project-references"></a>项目引用
 面向 Windows 10 的通用 Windows 平台 (UWP) 项目可以创建对解决方案中其他 UWP 项目的引用，也可以创建对面向 [!INCLUDE[win81](../includes/win81-md.md)]的 Windows 应用商店项目或二进制文件的引用，前提是这些项目不使用 Windows 10 中已弃用的 API。 有关详细信息，请参阅 [从 Windows Runtime 8 移动到 UWP](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx)。

 如果选择将 [!INCLUDE[win81](../includes/win81-md.md)] 项目重定向到 Windows 10，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)

### <a name="extension-sdk-references"></a>扩展 SDK 引用
 面向通用 Windows 平台 (UWP) 的 Visual Basic、C#、C++ 和 JavaScript Windows 应用商店项目可以引用面向 [!INCLUDE[win81](../includes/win81-md.md)]的扩展 SDK，前提是这些扩展 SDK 不使用 Windows 10 中已弃用的 API。 请查看扩展 SDK 供应商站点，以确定它是否可由面向 UWP 的 Windows 应用商店项目进行引用。

 如果确定你的应用所引用的扩展 SDK 不受支持，则需执行以下步骤：

1. 查看导致错误的项目的名称。 项目所面向的平台记录在项目名称旁的括号中。 例如，“MyProjectName (Windows 8.1)” **** 表示项目 **MyProjectName** 面向平台版本 [!INCLUDE[win81](../includes/win81-md.md)]。

2. 转到拥有不受支持的扩展 SDK 的供应商站点，安装具有与你的项目所面向的平台版本兼容的依赖项的扩展 SDK 版本。

    > [!NOTE]
    > 找出扩展 SDK 与其他扩展 SDK 是否具有依赖关系的一种方法是：重新启动 Visual Studio，创建一个新的 C# Windows 应用商店项目，右键单击该项目并选择 **“添加引用”**，依次转到 **“Windows”** 选项卡和 **“扩展”** 子选项卡，然后选择该扩展 SDK 并查看 **“引用管理器”** 中的右窗格。 如果具有依赖关系，则将在该位置列出依赖关系。

    > [!IMPORTANT]
    > 如果你的项目面向 Windows 10，并且上一步中安装的扩展 SDK 在 Microsoft Visual C 运行时包上具有依赖关系，则与 Windows 10 兼容的 Microsoft Visual C++ 运行时包的版本为 v14.0，并与 Visual Studio 2015 一起安装。

3. 如果上一步中安装的扩展 SDK 在其他扩展 SDK 上具有依赖关系，请转到拥有依赖关系的供应商站点，并安装与你的项目所面向的平台版本相兼容的版本的依赖项。

4. 重启 Visual Studio 并打开你的应用。

5. 右键单击项目中导致错误的 "**引用**" 节点，然后选择 "**添加引用**"

6. 单击 " **Windows** " 选项卡，然后单击 " **扩展** " 子选项卡，然后取消选中旧扩展 sdk 的复选框，然后选中新扩展 sdk 的复选框。 单击" **确定**"。

## <a name="adding-a-reference-at-design-time"></a>在设计时添加引用
 当你对项目中的程序集进行引用时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 在以下位置搜索程序集：

- 当前项目目录。 （可以使用 **“浏览”** 选项卡查找这些程序集。）

- 同一解决方案中的其他项目目录。 （可以在 **“项目”** 选项卡上找到这些程序集。）

> [!NOTE]
> 所有项目都包含对 mscorlib 的隐式引用。 Visual Basic 项目包含对 `Microsoft.VisualBasic`的隐式引用。
>
> Visual Studio 中的所有项目都包含对 `System.Core`的隐式引用，即使 `System.Core` 已从引用列表中删除也是如此。

## <a name="references-to-shared-components-at-run-time"></a>在运行时对共享组件的引用
 在运行时，组件必须位于项目的输出路径或 [全局程序集缓存](https://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202) 中 (GAC) 。 如果项目中包含对某个对象的引用，但该对象不是上述的其中一个位置，则必须在生成项目时将该引用复制到项目的输出路径。 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 属性指示是否必须进行复制。 如果值为 **True**，则生成项目时，引用将复制到项目目录。 如果值为 **False**，则不复制引用。

 如果你部署的应用程序中包含对 GAC 中注册的自定义组件的引用，则无论采用何种 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 设置，组件都不会随应用程序一起部署。 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的早期版本中，可以在引用上设置 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 的属性，以确保程序集已部署。 现在，必须手动将程序集添加到 \Bin 文件夹。 这会对所有自定义代码进行详细审查，以降低你发布不熟悉的自定义代码的风险。

 默认情况下，如果程序集或组件位于全局程序集缓存中或者是框架组件，则 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> 属性设置为 **False** 。 否则，值设置为 **True**。 项目到项目的引用始终设置为 **True**。

## <a name="referencing-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>引用面向不同版本的 .NET Framework 的项目或程序集
 您可以创建一些应用程序，这些应用程序引用的项目或程序集面向 .NET Framework 的不同版本。 例如，您可以创建一个面向 [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] 的应用程序，该配置文件引用面向 [!INCLUDE[dnprdnext](../includes/dnprdnext-md.md)]的程序集。 如果创建的项目是面向 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]的早期版本，则不能在该项目中设置对面向 [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] 或 .NET Framework 版本 4 的项目或程序集的引用。

 有关详细信息，请参阅[面向特定的 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)。

## <a name="project-to-project-references"></a>项目到项目的引用
 项目到项目的引用是对包含程序集的项目的引用;可以通过使用 " **项目** " 选项卡来创建它们。 Visual Studio 可以在给定项目路径时找到程序集。

 如果拥有生成程序集的项目，则应引用该项目并且不使用文件引用（见下文）。 项目到项目的引用的一个优点是能够在生成系统中的项目之间创建依赖关系。 如果依赖项目在上次生成引用项目之后已发生更改，则将生成该依赖项目。 文件引用不会创建生成依赖关系，因此可以在不生成依赖项目的情况下生成引用项目，并且该引用可能会过时。 （也就是说，项目可以引用以前生成的项目版本。）这可能导致 bin 目录中所需的单个 DLL 同时存在多个版本，而这种情况实际是不可能出现的。 发生此冲突时，你将看到一条消息，如 [警告：无法将项目 "project" 中的依赖项 "file" 复制到运行目录，因为它将覆盖引用 "file](../misc/warning-the-dependency-file-in-project-project-cannot-be-copied.md)"。 有关详细信息，请参阅 [Troubleshooting Broken References](../ide/troubleshooting-broken-references.md) 和 [How to: Create and Remove Project Dependencies](../ide/how-to-create-and-remove-project-dependencies.md)。

> [!NOTE]
> 如果一个项目的目标 .NET Framework 版本是 4.5，而另一个项目的目标版本是 2、3、3.5 或 4.0，则创建的是文件引用而非项目到项目的引用。

## <a name="file-references"></a>文件引用
 文件引用是对 Visual Studio 项目上下文之外的程序集的直接引用；通过使用 **“引用管理器”** 中的 **“浏览”** 选项卡进行创建。 当只有程序集或组件，而没有将其创建为输出的项目时，则使用文件引用。

## <a name="see-also"></a>另请参阅
 [排查中断引用](../ide/troubleshooting-broken-references.md)[使用程序集编程](https://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)[如何：使用引用管理器添加或删除引用](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)
