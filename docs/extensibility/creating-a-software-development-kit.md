---
title: 创建软件开发工具包 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61e547be5f240cafccc058eb7ea2249fd492554b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904120"
---
# <a name="create-a-software-development-kit"></a>创建软件开发工具包

软件开发工具包（SDK）是一系列 Api，你可以在 Visual Studio 中将其作为单个项引用。 "**引用管理器**" 对话框将列出与项目相关的所有 sdk。 将 SDK 添加到项目时，Api 在 Visual Studio 中可用。

有两种类型的 Sdk：

- 平台 Sdk 是用于为平台开发应用程序的必需组件。 例如， [!INCLUDE[win81](../debugger/includes/win81_md.md)] 需要 SDK 来开发 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用。

- 扩展 Sdk 是扩展平台的可选组件，但不是为该平台开发应用程序所必需的。

以下各节介绍了 Sdk 的通用基础结构，以及如何创建平台 SDK 和扩展 SDK。

## <a name="platform-sdks"></a>平台 SDK

开发平台应用需要平台 Sdk。 例如， [!INCLUDE[win81](../debugger/includes/win81_md.md)] 需要 SDK 来开发适用于的应用程序 [!INCLUDE[win81](../debugger/includes/win81_md.md)] 。

### <a name="installation"></a>安装

所有平台 Sdk 都将安装在*HKLM\Software\Microsoft\Microsoft sdk \\ [TPI] \V [TPV] \\ @InstallationFolder = [SDK root]* 上。 相应地， [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK 安装在*HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1*。

### <a name="layout"></a>布局

平台 Sdk 具有以下布局：

```
\[InstallationFolder root]
            SDKManifest.xml
            \References
                  \[config]
                        \[arch]
            \DesignTime
                  \[config]
                        \[arch]
```

| 节点 | 说明 |
|------------------------| - |
| *引用*文件夹 | 包含二进制文件，这些二进制文件包含可针对编写的 Api。 其中可能包括 Windows 元数据（WinMD）文件或程序集。 |
| *DesignTime*文件夹 | 包含仅在运行前/调试时需要的文件。 其中可能包括 XML 文档、库、标头、工具箱设计时二进制文件、MSBuild 项目等等<br /><br /> 理想情况下，XML 文档将放置在*\DesignTime*文件夹中，但引用的 xml 文档将继续与 Visual Studio 中的引用文件放置在一起。 例如，引用<em>\References \\ [config] \\ [\sample.xml\sample.dll</em>的 XML 文档将是*\References \\ [config] \\ [] *，而该文档的本地化版本将为*\References \\ [config] [] \\ \\ [locale] \sample.xml*。 |
| *配置*文件夹 | 只能有三个文件夹： "*调试*"、"*零售*" 和 " *CommonConfiguration*"。 如果应使用相同的一组 SDK 文件，SDK 作者可以将其文件放在*CommonConfiguration*下，而不管 sdk 使用者将面向的配置如何。 |
| *体系结构*文件夹 | 任何受支持的*体系结构*文件夹都可能存在。 Visual Studio 支持以下体系结构： x86、x64、ARM 和非特定语言。 注意： Win32 映射到 x86，而 AnyCPU 映射到非特定语言。<br /><br /> MSBuild 仅在适用于平台 Sdk 的*\CommonConfiguration\neutral*下显示。 |
| *SDKManifest.xml* | 此文件介绍 Visual Studio 应如何使用 SDK。 查看以下 SDK 清单 [!INCLUDE[win81](../debugger/includes/win81_md.md)] ：<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName：** 对象浏览器在 "浏览" 列表中显示的值。<br /><br /> **PlatformIdentity：** 此属性的存在会告诉 Visual Studio 和 MSBuild，SDK 是平台 SDK，不应在本地复制从它添加的引用。<br /><br /> **TargetFramework：** 此属性由 Visual Studio 用于确保只有面向此属性值中指定的相同框架的项目才能使用 SDK。<br /><br /> **MinVSVersion：** Visual Studio 使用此属性来仅使用适用于它的 Sdk。<br /><br /> **参考：** 必须仅为包含控件的引用指定此属性。 有关如何指定引用是否包含控件的信息，请参阅下面的。 |

## <a name="extension-sdks"></a>扩展 SDK

以下各节介绍了部署扩展 SDK 需要执行的操作。

### <a name="installation"></a>安装

可以为特定用户或所有用户安装扩展 Sdk，无需指定注册表项。 若要为所有用户安装 SDK，请使用以下路径：

*% Program Files%\Microsoft Sdk \<target platform\> \v<平台版本号 \> \ExtensionSDKs*

对于用户特定的安装，请使用以下路径：

*%USERPROFILE%\AppData\Local\Microsoft Sdk \<target platform\> \v<平台版本号 \> \ExtensionSDKs*

如果要使用其他位置，则必须执行以下两个操作之一：

1. 在注册表项中指定：

     **HKLM\Software\Microsoft\Microsoft Sdk \<target platform> \v<平台版本号 \> \ExtensionSDKs\<SDKName>\<SDKVersion>**\

     并添加一个值为的（默认）子项 `<path to SDK><SDKName><SDKVersion>` 。

2. 将 MSBuild 属性添加 `SDKReferenceDirectoryRoot` 到项目文件。 此属性的值是一个以分号分隔的目录列表，其中包含要引用的扩展 Sdk。

### <a name="installation-layout"></a>安装布局

扩展 Sdk 具有以下安装布局：

```
\<ExtensionSDKs root>
           \<SDKName>
                 \<SDKVersion>
                        SDKManifest.xml
                        \References
                              \<config>
                                    \<arch>
                        \Redist
                              \<config>
                                    \<arch>
                        \DesignTime
                               \<config>
                                     \<arch>

```

1. \\<SDKName \> \\<SDKVersion \> ：扩展 sdk 的名称和版本从 SDK 根路径中的相应文件夹名称派生而来。 MSBuild 使用此标识在磁盘上查找 SDK，Visual Studio 在 "**属性**" 窗口和 "**引用管理器**" 对话框中显示此标识。

2. *引用*文件夹：包含 api 的二进制文件。 这些文件可以是 Windows 元数据（WinMD）文件或程序集。

3. 再*发行*文件夹：运行时/调试所需的文件，应打包为用户应用程序的一部分。 所有二进制文件都应放置在*\redist \\<config \> \\<\> *下，二进制名称应采用以下格式，以确保唯一性： *]* \<company> ... \<product> \<purpose> \<extension><em>.例如，* Microsoft.Cpp.Build.dll</em>。 所有名称与其他 Sdk 中的文件名（例如 javascript、css、pri、xaml、png 和 jpg 文件）都不应放置在 \redist<<<config 下的所有文件（如<em> \\ \> \\ \> \\ \> \* 与 xaml 控件关联的文件除外）。应将这些文件放在 * \redist \\<config \> \\<\> \\<componentname \> \\ 下</em>。

4. *DesignTime*文件夹：只需预运行/调试时间所需的文件，不应将其打包为用户的应用程序的一部分。 它们可以是 XML 文档、库、标头、工具箱设计时二进制文件、MSBuild 项目等。 旨在供本机项目使用的任何 SDK 都必须有*SDKName 属性*文件。 下面显示了此类型文件的示例。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <ExecutablePath>C:\Temp\ExecutablePath;$(ExecutablePath)</ExecutablePath>
       <IncludePath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\CommonConfiguration\Neutral\include;$(IncludePath)</IncludePath>
       <AssemblyReferencePath>C:\Temp\AssemblyReferencePath;(AssemblyReferencePath)</AssemblyReferencePath>
       <LibraryPath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\Debug\ARM;$(LibraryPath)</LibraryPath>
       <SourcePath>C:\Temp\SourcePath\X64;$(SourcePath)</SourcePath>
       <ExcludePath>C:\Temp\ExcludePath\X64;$(ExcludePath)</ExcludePath>
       <_PropertySheetDisplayName>DevILSDK, 1.0</_PropertySheetDisplayName>
     </PropertyGroup>
   </Project>

   ```

    XML 引用文档与引用文件放在一起。 例如， *\References \\<config \> \\<拱 \>\sample.dll*程序集的 XML 引用文档为*\References \\<config \> \\ \> *<！，而该文档的本地化版本*\References \\\sample.xml\> \\ \> \\ \> *<<<\sample.xml

5. *配置*文件夹：三个子文件夹：*调试*、*零售*和*CommonConfiguration*。 当使用相同的一组 SDK 文件时，SDK 作者可以将其文件放在*CommonConfiguration*下，而不管 sdk 使用者的目标配置如何。

6. *体系结构*文件夹：支持以下体系结构： x86、X64、ARM、非特定语言。 Win32 映射到 x86，而 AnyCPU 映射到非特定语言。

### <a name="sdkmanifestxml"></a>SDKManifest.xml

*SDKManifest.xml*文件描述了 Visual Studio 应如何使用 SDK。 下面是一个示例：

```
<FileList>
DisplayName = "My SDK"
ProductFamilyName = "My SDKs"
TargetFramework = ".NETCore, version=v4.5.1; .NETFramework, version=v4.5.1"
MinVSVersion = "14.0"
MaxPlatformVersion = "8.1"
AppliesTo = "WindowsAppContainer + WindowsXAML"
SupportPrefer32Bit = "True"
SupportedArchitectures = "x86;x64;ARM"
SupportsMultipleVersions = "Error"
CopyRedistToSubDirectory = "."
DependsOn = "SDKB, version=2.0"
MoreInfo = "https://msdn.microsoft.com/MySDK">
<File Reference = "MySDK.Sprint.winmd" Implementation = "XNASprintImpl.dll">
<Registration Type = "Flipper" Implementation = "XNASprintFlipperImpl.dll" />
<Registration Type = "Flexer" Implementation = "XNASprintFlexerImpl.dll" />
<ToolboxItems VSCategory = "Toolbox.Default" />
</File>
</FileList>
```

下面的列表提供了文件的元素：

1. DisplayName：在引用管理器中显示的值，解决方案资源管理器、对象浏览器和 Visual Studio 用户界面中的其他位置。

2. ProductFamilyName：总体 SDK 产品名称。 例如， [!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] sdk 名为 "WinJS" 和 "WinJS"，属于同一系列 SDK 产品系列，即 "WinJS" 中的 ""。 此特性允许 Visual Studio 和 MSBuild 进行该连接。 如果此属性不存在，则将 SDK 名称用作产品系列名称。

3. FrameworkIdentity：指定一个或多个 Windows 组件库的依赖项。 此属性的值将放入正在使用的应用的清单中。 此属性仅适用于 Windows 组件库。

4. TargetFramework：指定在 "引用管理器" 和 "工具箱" 中可用的 Sdk。 这是一个以分号分隔的目标框架名字对象的列表，例如 ".NET Framework，version = v2.0; .NET Framework，version = v1.0"。 如果指定了多个版本的相同目标框架，则引用管理器将使用指定的最低版本进行筛选。 例如，如果指定了 ".NET Framework，version = v2.0; .NET Framework，version = v 4.5.1"，则引用管理器将使用 ".NET Framework，version = v2.0"。 如果指定了特定目标框架配置文件，则引用管理器将仅使用该配置文件进行筛选。 例如，如果指定了 "Silverlight，version = v4.0，profile = WindowsPhone"，则仅 Windows Phone 配置文件上的参考管理器筛选器;面向完整 Silverlight 4.0 Framework 的项目在引用管理器中看不到 SDK。

5. MinVSVersion：最低 Visual Studio 版本。

6. MaxPlatformVerson：应使用最大目标平台版本来指定扩展 SDK 将无法在其上运行的平台版本。 例如，Microsoft Visual C++ 运行时包版本11.0 应仅由 Windows 8 项目引用。 因此，Windows 8 项目的 MaxPlatformVersion 为8.0。 这意味着，引用管理器会筛选出 Windows 8.1 项目 Microsoft Visual C++ 运行时包，而当项目引用该项目时，MSBuild 将引发错误 [!INCLUDE[win81](../debugger/includes/win81_md.md)] 。 注意：从开始，支持此元素 [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] 。

7. AppliesTo：通过指定适用的 Visual Studio 项目类型来指定引用管理器中可用的 Sdk。 可识别九个值： WindowsAppContainer、VisualC、VB、CSharp、WindowsXAML、JavaScript、托管和本机。 SDK 作者可以使用 and （"+"）、or （"&#124;"）而不是（"！"）用于精确指定应用于 SDK 的项目类型范围的运算符。

    WindowsAppContainer 标识应用的项目 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 。

8. SupportPrefer32Bit：支持的值为 "True" 和 "False"。 默认值为 "True"。 如果此值设置为 "False"， [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 则如果引用 SDK 的项目已启用 Prefer32Bit，则 MSBuild 将返回项目的错误（或桌面项目的警告）。 有关 Prefer32Bit 的详细信息，请参阅 "[生成" 页、项目设计器（c #）](../ide/reference/build-page-project-designer-csharp.md)或["编译" 页、项目设计器（Visual Basic）](../ide/reference/compile-page-project-designer-visual-basic.md)。

9. SupportedArchitectures：以分号分隔的 SDK 支持的体系结构列表。 如果不支持使用项目中的目标 SDK 体系结构，MSBuild 将显示警告。 如果未指定此属性，则 MSBuild 永远不会显示此类警告。

10. SupportsMultipleVersions：如果此属性设置为 "**错误**" 或 "**警告**"，则 MSBuild 将指示同一个项目无法引用同一 SDK 系列的多个版本。 如果此属性不存在或设置为 "**允许**"，则 MSBuild 不会显示此类型的错误或警告。

11. AppX：指定磁盘上 Windows 组件库的应用包的路径。 在本地调试期间，此值将传递给 Windows 组件库的注册组件。 文件名的命名约定为* \<Company> ... \<Product> 。 \<Architecture> \<Configuration> \<Version>appx*。 如果属性名称和属性值不适用于 Windows 组件库，则配置和体系结构是可选的。 此值仅适用于 Windows 组件库。

12. CopyRedistToSubDirectory：指定应相对于应用程序包根（即，在 "**创建应用包**" 向导中选择的**包位置**）和 "运行时布局根" 复制*\redist*文件夹下的文件的位置。 默认位置是应用包和**F5**布局的根。

13. DependsOn：一系列 SDK 标识，用于定义此 SDK 依赖的 sdk。 此属性显示在 "引用管理器" 的 "详细信息" 窗格中。

14. MoreInfo：指向提供帮助和详细信息的网页的 URL。 此值用在引用管理器右窗格的 "详细信息" 链接中。

15. 注册类型：指定应用程序清单中的 WinMD 注册，它是本机 WinMD 必需的，具有对应的实现 DLL。

16. 文件引用：仅为包含控件的引用或本机 Winmd 指定。 有关如何指定引用是否包含控件的信息，请参阅下面的[指定工具箱项的位置](#ToolboxItems)。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a>指定工具箱项的位置

*SDKManifest.xml*架构的**ToolBoxItems**元素指定平台和扩展 sdk 中的工具箱项的类别和位置。 下面的示例演示如何指定不同的位置。 这适用于 WinMD 或 DLL 引用。

1. 将控件置于 "工具箱" 的 "默认" 类别。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. 将控件置于特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory= "MyCategoryName"/>
    </File>
    ```

3. 将控件置于特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems VSCategory = "Data">
        <ToolboxItems />
    </File>
    ```

4. 将不同类别名称下的控件置于 Blend 和 Visual Studio 中。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. 以不同的方式枚举 Blend 和 Visual Studio 中的特定控件。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. 枚举特定的控件，并将它们放在 Visual Studio 公用路径下，或仅置于 "所有控件" 组中。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. 枚举特定的控件，并在 ChooseItems 中仅显示特定集，而不会在工具箱中显示它们。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>另请参阅

- [演练：使用 c + + 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [演练：使用 c # 或 Visual Basic 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [管理项目中的引用](../ide/managing-references-in-a-project.md)
