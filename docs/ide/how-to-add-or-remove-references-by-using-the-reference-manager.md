---
title: 在引用管理器中添加引用
ms.date: 08/02/2019
ms.topic: conceptual
f1_keywords:
- VS.ReferenceManager
helpviewer_keywords:
- C# projects, references
- references [Visual Studio], adding
- assemblies [Visual Studio], references
- Visual Basic projects, references
- project references, adding
- referencing components, adding references
- project references, removing
- referencing assemblies
- referencing components, removing references
- references [Visual Studio], removing
- referencing components, assemblies not listed
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e302b5c4df73f8fcdadf766a1fe1d8dc0731c261
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654827"
---
# <a name="how-to-add-or-remove-references-by-using-the-reference-manager"></a>如何：使用引用管理器添加或删除引用

可以使用“引用管理器”对话框添加和管理对你、Microsoft 或其他公司开发的组件的引用。 如果要开发通用 Windows 应用，你的项目将自动引用所有正确的 Windows SDK DLL。 如果要开发 .NET 应用程序，你的项目将自动引用 mscorlib.dll  。 一些 .NET API 在必须手动添加的组件中进行公开。 对 COM 组件或自定义组件的引用必须手动添加。

## <a name="reference-manager-dialog-box"></a>“引用管理器”对话框

“引用管理器”对话框在左侧显示不同类别，具体取决于项目类型：

- **程序集**，包含“框架”和“扩展”子组  

- **COM**，列出可供引用的所有 COM 组件

- **项目**

- **共享项目**

- **Windows**，包含“核心”和“扩展”子组   。 可以使用“对象浏览器”  浏览 Windows SDK 或扩展 SDK 中的引用。

- **浏览**，包含“最近”子组 

## <a name="add-a-reference"></a>添加引用

1. 在“解决方案资源管理器”中，右键单击“引用”或“依赖项”节点，然后选择“添加引用”     。 还可以右键单击项目节点，然后选择“添加” > “引用”   。

   此时将打开“引用管理器”  ，并按组列出可用引用。

2. 指定要添加的引用，然后选择“确定”  。

## <a name="assemblies-tab"></a>“程序集”选项卡

“程序集”选项卡中列出了可引用的所有 .NET 程序集  。 “程序集”选项卡不会列出全局程序集缓存 (GAC) 中的任何程序集，因为 GAC 中的程序集是运行时环境的一部分  。 如果某个应用程序包含对在 GAC 中注册的程序集的引用，则在部署或复制该应用程序时，无论“复制本地”设置为何，所引用的程序集都不会与该应用程序一起部署或复制  。 有关详细信息，请参阅[管理项目中的引用](../ide/managing-references-in-a-project.md)。

在手动添加对任何 EnvDTE 命名空间（<xref:EnvDTE>、<xref:EnvDTE80>、<xref:EnvDTE90>、<xref:EnvDTE90a> 或 <xref:EnvDTE100>）的引用时，请在“属性”窗口中将引用的“嵌入互操作类型”属性设置为“False”    。 将此属性设置为“True”  可能会导致生成问题，因为某些 EnvDTE 属性无法嵌入。

所有桌面项目都包含对 mscorlib 的隐式引用  。 Visual Basic 项目包含对 <xref:Microsoft.VisualBasic> 的隐式引用。 即使已将 System.Core 从引用列表删除，所有项目仍包含对其的隐式引用  。

如果项目类型不支持程序集，则此选项卡不会显示在“引用管理器”对话框中。

“程序集”选项卡包含两个子选项卡  ：

1. “框架”列出组成目标框架的所有程序集  。

   对于不面向 .NET Core 或通用 Windows 平台的项目，“框架”选项卡中枚举了目标框架中的程序集  。 用户必须添加应用程序所需的任何引用。

   通用 Windows 项目默认包含对目标框架中所有程序集的引用。 在托管项目中，“解决方案资源管理器”的“引用”文件夹下的只读节点表示对整个框架的引用   。 因此，“框架”选项卡不枚举框架中的任何程序集，而是显示以下消息  ：“已引用所有框架程序集。 请使用对象浏览器浏览框架中的引用”。

2. “扩展”列出了组件和控件的外部供应商为扩展目标框架而开发的所有程序集  。 根据用户应用程序的用途，可能需要这些程序集。

   “扩展”通过枚举在以下位置注册的程序集来填充  ：

   32 位计算机：
   - `HKEY_CURRENT_USER\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   64 位计算机：
   - `HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   [目标框架标识符]的旧版本

   例如，如果项目面向 32 位计算机上的 .NET Framework 4，则“扩展”将枚举在 \Microsoft\.NETFramework\v4.0\AssemblyFoldersEx、\Microsoft\.NETFramework\v3.5\AssemblyFoldersEx、\Microsoft\.NETFramework\v3.0\AssemblyFoldersEx 和 \Microsoft\.NETFramework\v2.0\AssemblyFoldersEx 下注册的程序集      。

列表中的某些组件可能不会显示，具体取决于项目的框架版本。 在下列条件下，可能会出现这种情况：

- 使用最新框架版本的组件与面向早期版本的项目不兼容。

   有关如何更改项目的目标框架版本的信息，请参阅[框架目标概述](visual-studio-multi-targeting-overview.md)。

- 使用 .NET Framework 4 的组件与面向 .NET Framework 4.5 的项目不兼容。

应当避免添加对同一解决方案中另一个项目的输出的文件引用，因为这样做可能导致编译错误。 而应使用“添加引用”  对话框的“项目”  选项卡来创建项目到项目的引用。 这样就可以更好地管理在项目中创建的类库，从而更易于进行团队开发。 有关详细信息，请参阅[有关无效引用的疑难解答](../ide/troubleshooting-broken-references.md)。

> [!NOTE]
> 在 Visual Studio 2015 或更高版本中，如果一个项目的目标框架版本为 .NET Framework 4.5 或更高版本，而另一个项目的目标版本为 .NET Framework 2、3、3.5 或 4.0，则将创建文件引用而不是项目引用。

### <a name="to-display-an-assembly-in-the-add-reference-dialog-box"></a>在“添加引用”对话框中显示程序集

- 将程序集移动或复制到下列位置之一：

  - 当前项目目录。 （可以使用 **“浏览”** 选项卡查找这些程序集。）

  - 同一解决方案中的其他项目目录。 （可以使用“项目”  选项卡查找这些程序集。）

  \- 或 -

- 设置指定要显示的程序集位置的注册表项：

  对于 32 位操作系统，添加以下注册表项之一。

  - `[HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  对于 64 位操作系统，在 32 位注册表配置单元中添加以下注册表项之一。

  - `[HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  \<VersionMinimum\> 是所应用的最低框架版本  。 如果 \<VersionMinimum\> 为 v3.0，则 AssemblyFoldersEx 中指定的文件夹应用于以 3.0 版本及更高版本的 .NET Framework 为目标的项目   。

  \<AssemblyLocation\> 是要在“添加引用”对话框中显示的程序集目录，例如 C:\MyAssemblies    。

  通过在 `HKEY_LOCAL_MACHINE` 节点下创建注册表项，所有用户都可以在“添加引用”对话框中的指定位置看到这些程序集  。 在 `HKEY_CURRENT_USER` 节点下创建注册表项只会影响当前用户的设置。

  再次打开“添加引用”  对话框。 程序集应出现在“.NET”  选项卡中。如果未显示，请确保这些程序集位于指定的 AssemblyLocation  目录中，然后重启 Visual Studio 并重试。

## <a name="projects-tab"></a>“项目”选项卡

在“解决方案”子选项卡中，“项目”选项卡列出当前解决方案中的所有兼容项目   。

一个项目可以引用面向其他框架版本的另一个项目。 例如，可以创建一个面向 .NET Framework 4、但引用针对 .NET Framework 2 生成的程序集的项目。 不过，.NET Framework 2 项目不能引用 .NET Framework 4 项目。 有关详细信息，请参阅[框架定位概述](../ide/visual-studio-multi-targeting-overview.md)。

> [!NOTE]
> 面向 NET Framework 4 的项目与面向 .NET Framework 4 Client Profile 的项目不兼容。

## <a name="shared-projects-tab"></a>“共享项目”选项卡

在“引用管理器”对话框的“共享项目”选项卡上添加对共享项目的引用  。 使用[共享项目](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)，可以编写由多个不同的应用程序项目引用的通用代码。

## <a name="universal-windows-tab"></a>通用 Windows 选项卡

“通用 Windows”选项卡列出特定于运行 Windows 操作系统的平台的所有 SDK  。
此选项卡具有两个子组：“核心”与“扩展”   。

### <a name="core-subgroup"></a>“核心”子组

默认情况下，通用 Windows 应用项目具有对通用 Windows SDK 的引用。 因此，“引用管理器”中的“核心”子组不枚举通用 Windows SDK 的任何程序集   。

### <a name="extensions-subgroup"></a>“扩展”子组

“扩展”列出用于扩展目标 Windows 平台的用户 SDK  。

SDK 是文件集合，Visual Studio 将其视为单个组件。 在“扩展”选项卡中，应用于调用了“引用管理器”对话框的项目的 SDK 将作为单个项列出  。 添加到项目时，所有 SDK 内容将由 Visual Studio 使用，这样，用户无需采取任何额外操作即可使用 IntelliSense、工具箱、设计器、对象浏览器、生成、部署、调试和打包中的 SDK 内容。

若要了解如何在“扩展”选项卡中显示 SDK，请参阅[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)  。

> [!NOTE]
> 如果项目引用的 SDK 依赖于另一 SDK，则只有在用户手动添加对另一 SDK 的引用后，Visual Studio 才会使用另一 SDK。 当用户在“扩展”选项卡上选择 SDK 时，“引用管理器”对话框会在详细信息窗格中列出所有依赖项，从而帮助你找出 SDK 依赖项  。

如果项目类型不支持扩展，则此选项卡不会显示在“引用管理器”对话框中。

## <a name="com-tab"></a>“COM”选项卡

“COM”选项卡列出可供引用的所有 COM 组件  。 如果要添加对包含内部清单的已注册 COM DLL 的引用，请先注销该 DLL。 否则，Visual Studio 会将程序集引用作为 ActiveX 控件而不是本机 DLL 添加。

如果项目类型不支持 COM，则此选项卡不会显示在“引用管理器”对话框中。

## <a name="browse"></a>浏览

可以使用“浏览”  按钮浏览查找文件系统中的组件。

一个项目可以引用面向其他框架版本的组件。 例如，可以创建一个面向 .NET Framework 4.7、但引用面向 .NET Framework 4 的组件的应用程序。 有关详细信息，请参阅[框架定位概述](../ide/visual-studio-multi-targeting-overview.md)。

避免在同一个解决方案中添加对另一个项目的输出的文件引用，因为这可能导致编译错误。 而应使用“引用管理器”对话框的“解决方案”  选项卡来创建项目到项目的引用。 这样就可以更好地管理在项目中创建的类库，从而更易于进行团队开发。 有关详细信息，请参阅[有关无效引用的疑难解答](../ide/troubleshooting-broken-references.md)。

无法浏览到 SDK 并将其添加到项目。 只能浏览到文件（例如程序集或 .winmd）并将其添加到项目  。

执行对 WinMD 的文件引用时，预期布局为 \<FileName>.winmd、\<FileName>.dll 和 \<FileName>.pri 文件全部并排放置    。 如果在以下情况下引用 WinMD，一组不完整的文件将复制到项目输出目录中，从而导致生成和运行时失败。

- **本机组件**：本机项目将为每个不相交的命名空间集创建一个 WinMD 以及一个包含实现的 DLL。 WinMD 将具有不同的名称。 引用此本机组件文件时，MSBuild 不会将名称不同的 WinMD 视为一个组件。 因此，将仅复制名称相同的 \<FileName>.dll 和 \<FileName>.winmd，并且将发生运行时错误   。 若要解决此问题，请创建扩展 SDK。 有关详细信息，请参阅[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)。

- 使用控件：XAML 控件至少包含一个 \<FileName>.winmd、一个 \<FileName>.dll、一个 \<FileName>.pri、一个 \<XamlName>.xaml 和一个 \<ImageName>.jpg       。 生成项目时，与文件引用关联的资源文件不会复制到项目的输出目录中，将仅复制 \<FileName>.winmd、\<FileName>.dll 和 \<FileName>.pri    。 将记录一个生成错误，通知用户缺少 \<XamlName>.xaml 和 \<ImageName>.jpg 资源   。 若要成功，用户必须将这些资源文件手动复制到项目输出目录以用于生成和调试/运行时。 若要解决此问题，请按照[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)中的步骤创建扩展 SDK，或编辑项目文件，添加以下属性：

    ```xml
    <PropertyGroup>
       <GenerateLibraryOutput>True</GenerateLibraryOutput>
    </PropertyGroup>
    ```

    > [!NOTE]
    > 如果添加属性，生成可能会运行较慢。

## <a name="recent"></a>Recent

“程序集”、“COM”、“Windows”和“浏览”均支持“最近”选项卡，此选项卡可枚举最近添加到项目的组件的列表      。

## <a name="search"></a>搜索

“引用管理器”对话框中的搜索栏在具有焦点的选项卡上运行。 例如，在“解决方案”选项卡具有焦点时，如果用户在搜索栏中键入“System”，则除非解决方案具有包含“System”的项目名称，否则搜索不会返回任何结果  。

## <a name="see-also"></a>请参阅

- [管理项目中的引用](../ide/managing-references-in-a-project.md)
