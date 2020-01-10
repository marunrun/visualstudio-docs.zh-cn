---
title: 如何：使用引用管理器添加或删除引用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ReferenceManager
helpviewer_keywords:
- Visual C# projects, references
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
ms.assetid: 1aabb520-99b0-46c6-9368-21b4d84793eb
caps.latest.revision: 48
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d0763f2cf86d94f96f6f9c907ee306c731994f22
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852093"
---
# <a name="how-to-add-or-remove-references-by-using-the-reference-manager"></a>如何：使用引用管理器添加或删除引用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用“引用管理器”对话框添加和管理对你、Microsoft 或其他公司开发的组件的引用。 如果要开发通用 Windows 应用，你的项目将自动引用所有正确的 Windows SDK DLL。 如果要开发 .NET 应用程序，你的项目将自动引用 mscorlib.dll。 一些 .NET API 在必须手动添加的组件中进行公开。 对 COM 组件或自定义组件的引用必须手动添加。

## <a name="adding-and-removing-a-reference"></a>添加和移除引用

#### <a name="to-add-a-reference"></a>添加引用

1. 在“解决方案资源管理器”中，右键单击“引用”节点，然后选择“添加引用”。

2. 指定要添加的引用，然后选择“确定”按钮。

   此时将打开“引用管理器”，并按组列出可用引用。 项目类型确定将显示以下哪一组：

- “程序集”组，包含“框架”和“扩展”子组。

- “解决方案”组，包含“项目”子组。

- “Windows”组，包含“核心”和“扩展”子组。 可以使用“对象浏览器”浏览 Windows SDK 或扩展 SDK 中的引用。

- “浏览”组，包含“最近”子组。

## <a name="assemblies-tab"></a>“程序集”选项卡
 “程序集”选项卡列出可供引用的所有 .NET Framework 程序集。 “程序集”选项卡不会列出全局程序集缓存 (GAC) 中的任何程序集，这是因为 GAC 中的程序集是运行时环境的一部分。 如果某个应用程序包含对在 GAC 中注册的程序集的引用，则在部署或复制该应用程序时，无论“复制本地”设置为何，所引用的程序集都不会与该应用程序一起部署或复制。 有关详细信息，请参阅[项目引用](https://msdn.microsoft.com/library/ez524kew.aspx)。

 在添加对任何 EnvDTE 命名空间（EnvDTE、EnvDTE80、EnvDTE90、EnvDTE90a 或 EnvDTE100）的引用时，请在“属性”窗口中将引用的“嵌入互操作类型”属性设置为“False”。 将此属性设置为“True”可能会导致生成问题，因为某些 EnvDTE 属性是不能嵌入的。

 所有桌面项目都包含对 mscorlib 的隐式引用。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目包含对 Microsoft.VisualBasic 的隐式引用。 在 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 中，所有项目都包含对 System.Core 的隐式引用，即使从引用列表中移除了 System.Core 也是如此。

 如果项目类型不支持程序集，则此选项卡不会显示在“引用管理器”对话框中。

 “程序集”选项卡包含两个子选项卡：

1. “框架”列出组成目标框架的所有程序集。

   - 当你的项目以目标框架的配置文件为目标时，公布的程序集在完整框架中并在“框架”列表中枚举。 公布的程序集显示为灰色，以便与项目的目标框架配置文件中存在的程序集区分。 例如，如果项目以 .NET Framework 4 Client 为目标，“框架”列表将显示 .NET Framework 4 中的公布程序集。 用户添加已公布的程序集时，在“引用管理器”对话框关闭后，用户将收到通知，表明项目将重定目标为 .NET Framework 4，并将添加已公布的程序集。

   - 默认情况下，针对 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用的项目在项目创建时包含对目标[!INCLUDE[net_win8_profile](../includes/net-win8-profile-md.md)] 中所有程序集的引用。 在托管项目中，“解决方案资源管理器”中“引用”文件夹下的只读节点指示对整个框架的引用。 因此，“框架”选项卡不从框架枚举任何程序集，而是显示以下消息：“已引用所有框架程序集。 请使用对象浏览器浏览框架中的引用。” 对于桌面项目，“框架”选项卡枚举目标框架中的程序集，用户必须添加应用程序所需的引用。

2. “扩展”列出了组件和控件的外部供应商为扩展目标框架而开发的所有程序集。 根据用户应用程序的用途，可能需要这些程序集。

   - “扩展”通过枚举在以下位置注册的程序集来填充：

       ```
       32-bit machine:
       HKEY_CURRENT_USER\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       64-bit machine:
       HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       And older versions of the [Target Framework Identifier]
       ```

        例如，如果项目以 32 位计算机上的 .NET Framework 4 为目标，则“扩展”将枚举在 \Microsoft\\.NETFramework\v4.0\AssemblyFoldersEx\\、\Microsoft\\.NETFramework\v3.5\AssemblyFoldersEx\\、Microsoft\\.NETFramework\v3.0\AssemblyFoldersEx\\ 和 \Microsoft\\.NETFramework\v2.0\AssemblyFoldersEx\\ 下注册的程序集。

   列表中的一些组件可能不会显示，具体取决于项目的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。 在下列条件下，可能会出现这种情况：

- 使用最新版本的 .NET Framework 的组件与以早期版本的 .NET Framework 为目标的项目不兼容。

     若要深入了解如何更改项目的目标 .NET Framework 版本，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

- 使用 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 的组件与以 [!INCLUDE[net_v45](../includes/net-v45-md.md)] 为目标的项目不兼容。

     当创建新的应用程序时，一些项目默认情况下以 [!INCLUDE[net_v45](../includes/net-v45-md.md)] 为目标。 有关详细信息，请参阅 [.NET Framework Client Profile](https://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1)。

- 应当避免添加对同一解决方案中另一个项目的输出的文件引用，因为这样做可能导致编译错误。 而应使用“添加引用”对话框的“项目”选项卡来创建项目到项目的引用。 这样就可以更好地管理在项目中创建的类库，从而更易于进行团队开发。 有关详细信息，请参阅[有关损坏的引用的疑难解答](../ide/troubleshooting-broken-references.md)。

- > [!NOTE]
    > 在 Visual Studio 2015 中，如果一个项目的 .NET Framework 目标版本为版本 4.5，而另一个项目的目标版本为版本 2、3、3.5 或 4.0，则将创建文件引用而不是项目引用。

#### <a name="to-display-an-assembly-in-the-add-reference-dialog-box"></a>在“添加引用”对话框中显示程序集

- 将程序集移动或复制到下列位置之一：

  - 当前项目目录。 （可以使用 **“浏览”** 选项卡查找这些程序集。）

  - 同一解决方案中的其他项目目录。 （可以使用“项目”选项卡查找这些程序集。）

    \- 或 -

- 设置指定要显示的程序集位置的注册表项：

   对于 32 位操作系统，添加以下注册表项之一。

  - [HKEY_CURRENT_USER\SOFTWARE\Microsoft\\.NETFramework\\VersionMinimum\AssemblyFoldersEx\MyAssemblies]@="AssemblyLocation"

  - [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\\VersionMinimum\AssemblyFoldersEx\MyAssemblies]@="AssemblyLocation"

    对于 64 位操作系统，在 32 位注册表配置单元中添加以下注册表项之一。

  - [HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\\VersionMinimum\AssemblyFoldersEx\MyAssemblies]@="AssemblyLocation"

  - [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\\VersionMinimum\AssemblyFoldersEx\MyAssemblies]@="AssemblyLocation"

    VersionMinimum 是适用的最低 .NET Framework 版本。 如果 VersionMinimum 为 v3.0，则在 AssemblyFoldersEx 中指定的文件夹适用于面向 .NET Framework 3.0 和更高版本的项目。

    AssemblyLocation 是要在“添加引用”对话框中显示的程序集目录，例如 C:\MyAssemblies\\。

    通过在 HKEY_LOCAL_MACHINE 节点下创建注册表项，所有用户都可以在“添加引用”对话框中的指定位置看到这些程序集。 如果在 HKEY_CURRENT_USER 节点下创建注册表项，则只会影响当前用户的设置。

    再次打开“添加引用”对话框。 程序集应出现在 " **.net** " 选项卡上。如果不是这样，请确保这些程序集位于指定的*AssemblyLocation*目录中，重新启动 Visual Studio，然后重试。

## <a name="com-tab"></a>“COM”选项卡
 “COM”选项卡列出可供引用的所有 COM 组件。 如果要添加对包含内部清单的已注册 COM DLL 的引用，请先注销该 DLL。 否则，Visual Studio 会将程序集引用作为 ActiveX 控件而不是本机 DLL 添加。

 如果项目类型不支持 COM，则此选项卡不会显示在“引用管理器”对话框中。

## <a name="solution-tab"></a>“解决方案”选项卡
 “解决方案”选项卡在“项目”子选项卡中列出当前解决方案中的所有兼容项目。

 一个项目可以引用以不同 .NET Framework 版本为目标的其他项目。 例如，可以创建一个以 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 为目标、但引用针对 .NET Framework 2 生成的程序集的项目。 不过，.NET Framework 2 项目不能引用 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 项目。 有关详细信息，请参阅[面向特定的 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)。

 以 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 为目标的项目与以 [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] 为目标的项目不兼容。

 在 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 中，如果一个项目以 .NET Framework 4 为目标，另一项目以早期版本为目标，则将创建文件引用而非项目引用。

 以[!INCLUDE[net_win8_profile](../includes/net-win8-profile-md.md)] 为目标的项目不能添加对以 .NET Framework 为目标的项目的项目引用，反之亦然。

## <a name="windows-tab"></a>“Windows”选项卡
 “Windows”选项卡列出特定于 Windows 操作系统运行所在平台的所有 SDK。

 可以通过两种方式在 Visual Studio 中生成 WinMD 文件：

- **[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用托管项目**：[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用项目可通过设置“项目属性”|“输出类型”=“WinMD 文件”来输出 WinMD 二进制文件。 WinMD 文件名必须是其中包含的所有命名空间的超集命名空间。 例如，如果项目包括命名空间 A.B 和 A.B.C，则其输出的 WinMD 的可能名称为 A.winmd 和 A.B.winmd。 如果用户输入与项目中的命名空间集不相交的“项目属性”|“程序集名称”或“项目属性”|“命名空间值”，或者项目中没有超集命名空间，则将生成一个生成警告：“A.winmd”不是此程序集的有效 .winmd 文件名。 Windows 元数据文件中的所有类型必须存在于文件名的子命名空间中。 无法在运行时查找文件名子命名空间中不存在的类型。 在此程序集中，最小的公共命名空间为“CSWSClassLibrary1”。 桌面 Visual Basic 或 Visual C# 项目只能使用通过 [!INCLUDE[win8](../includes/win8-md.md)] SDK 生成的 WinMD（也称为第一方 WinMD），无法生成 WinMD。

- **[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用本机项目**：本机 WinMD 文件仅包含元数据。 它的实现存在于单独 DLL 文件中。 若要生成本机二进制文件，可在“新建项目”对话框中选择“Windows 运行时组件”项目模板，或者从空项目开始并修改项目属性以生成 WinMD 文件。 如果项目中包含不相交的命名空间，则将出现生成错误，告知用户合并命名空间或运行 MSMerge 工具。

  “Windows”选项卡包括两个子组。

### <a name="core-subgroup"></a>“核心”子组
 “核心”子组列出目标 Windows 版本的 SDK 中的所有 WinMD（对于 Windows 运行时元素）。

 默认情况下，[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用项目在项目创建时包含对 [!INCLUDE[win8](../includes/win8-md.md)] SDK 中所有 WinMD 的引用。 在托管项目中，“解决方案资源管理器”中“引用”文件夹下的只读节点指示对整个 [!INCLUDE[win8](../includes/win8-md.md)] SDK 的引用。 因此，引用管理器中的“核心”子组不从 [!INCLUDE[win8](../includes/win8-md.md)] SDK 枚举任何程序集，而是显示消息：“已引用 Windows SDK。 请使用对象浏览器浏览 Windows SDK 中的引用”。

 在桌面项目中，默认情况下不显示“核心”子组。 若要添加 Windows 运行时，可打开项目节点的快捷菜单，选择“卸载项目”，添加以下代码片段，然后重新打开项目（在项目节点上选择“重新加载项目”）。 调用“引用管理器”对话框时，将显示“核心”子组。

```
<PropertyGroup>
  <TargetPlatformVersion>8.0</TargetPlatformVersion>
</PropertyGroup>
```

 请确保选中此子组上的“Windows”复选框。 随后应能使用 Windows 运行时元素。 但是，你还需要添加 System.Runtime，Windows 运行时从中定义在整个 Windows 运行库中使用的一些标准类和接口（例如 IEnumerable）。 若要了解如何添加 System.Runtime，请参阅[托管的桌面应用和 Windows 运行时](https://msdn.microsoft.com/library/windows/apps/jj856306.aspx#consuming_standard_windows_runtime_types)。

### <a name="extensions-subgroup"></a>“扩展”子组
 “扩展”列出用于扩展目标 Windows 平台的用户 SDK。 此选项卡仅针对 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]应用项目显示。 桌面项目不显示此选项卡，因为这些项目仅使用第一方 .winmd 文件。

 SDK 是文件集合，Visual Studio 将其视为单个组件。 在“扩展”选项卡中，应用于调用了“引用管理器”对话框的项目的 SDK 将作为单个项列出。 添加到项目时，所有 SDK 内容将由 Visual Studio 使用，这样，用户无需采取任何额外操作即可使用 IntelliSense、工具箱、设计器、对象浏览器、生成、部署、调试和打包中的 SDK 内容。 若要了解如何在“扩展”选项卡中显示 SDK，请参阅[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)。

> [!NOTE]
> 如果项目引用的 SDK 依赖于另一 SDK，则只有在用户手动添加对另一 SDK 的引用后，Visual Studio 才会使用另一 SDK。 用户在“扩展”选项卡上选择 SDK 时，“引用管理器”对话框不仅会列出此 SDK 的名称和版本，还会在详细信息窗格中列出所有 SDK 依赖项的名称，从而帮助用户确定 SDK 依赖项。 如果用户未注意到依赖项，仅添加此 SDK，MSBuild 将提示用户添加依赖项。

 如果项目类型不支持“扩展”，则此选项卡不会显示在“引用管理器”对话框中。

## <a name="browse-button"></a>“浏览”按钮
 可以使用“浏览”按钮浏览查找文件系统中的组件。

 一个项目可以引用以不同 .NET Framework 版本为目标的组件。 例如，可以创建以 .NET Framework 4 Client Profile 为目标，并引用以 .NET Framework 2 为目标的组件的应用程序。 有关详细信息，请参阅[面向特定的 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)。

 应当避免添加对同一解决方案中另一项目的输出的文件引用，因为这种做法可能导致编译错误。 而应使用“引用管理器”对话框的“解决方案”选项卡来创建项目到项目的引用。 这种做法可以更好地管理在项目中创建的类库，从而更易于进行团队开发。 有关详细信息，请参阅[有关损坏的引用的疑难解答](../ide/troubleshooting-broken-references.md)。

 无法浏览到 SDK 并将其添加到项目。 只能浏览到文件（例如程序集或 .winmd）并将其添加到项目。

 执行对 WinMD 的文件引用时，预期布局为 FileName.winmd、FileName.dll 和 FileName.pri 文件全部并排放置。 如果在以下情况下引用 WinMD，一组不完整的文件将复制到项目输出目录中，从而导致生成和运行时失败。

- **本机组件**：本机项目将为每个不相交的命名空间集创建一个 WinMD 以及一个包含实现的 DLL。 WinMD 将具有不同的名称。 引用此本机组件文件时，MSBuild 不会将名称不同的 WinMD 视为一个组件。 因此，将仅复制名称相同的 FileName.dll 和 FileName.winmd，并且将发生运行时错误。 若要解决此问题，请创建扩展 SDK。 有关详细信息，请参阅[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)。

- **使用控件**：XAML 控件至少包含一个 FileName.winmd、一个 FileName.dll、一个 FileName.pri、一个 XamlName.xaml 和一个 ImageName.jpg。 生成项目时，与文件引用关联的资源文件不会复制到项目的输出目录中，将仅复制 FileName.winmd、FileName.dll 和 FileName.pri。 将记录一个生成错误，通知用户缺少 XamlName.xaml 和 ImageName.jpg 资源。 若要成功，用户必须将这些资源文件手动复制到项目输出目录以用于生成和调试/运行时。 若要解决此问题，请按照[创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)中的步骤创建扩展 SDK，或编辑项目文件，添加以下属性：

    ```
    <PropertyGroup>
    <GenerateLibraryOutput>True</GenerateLibraryOutput>
    </PropertyGroup>
    ```

    > [!NOTE]
    > 如果添加属性，生成可能会运行较慢。

## <a name="recent"></a>Recent
 “程序集”、“COM”、“Windows”和“浏览”均支持“最近”选项卡，此选项卡可枚举最近添加到项目的组件的列表。

## <a name="search"></a>搜索
 “引用管理器”对话框中的搜索栏在处于焦点的选项卡上运行。 例如，在“解决方案”选项卡处于焦点时，如果用户在搜索栏中键入“System”，则除非解决方案具有包含“System”的项目名称，否则搜索不会返回任何结果。

## <a name="see-also"></a>请参阅
 [笔尖如何：使用 "添加引用" 对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)[在项目中管理引用](../ide/managing-references-in-a-project.md)
