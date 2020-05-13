---
title: 创建软件开发工具包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f7cf6cf092edf96280c566018231cc00d34c0994
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739601"
---
# <a name="create-a-software-development-kit"></a>创建软件开发工具包

软件开发工具包 （SDK） 是 API 的集合，您可以将其作为 Visual Studio 中的单个项目引用。 "**参考管理器**"对话框列出了与项目相关的所有 SDK。 将 SDK 添加到项目时，API 可在可视化工作室中使用。

有两种类型的 SDK：

- 平台 SDK 是开发平台应用的必填组件。 例如，SDK[!INCLUDE[win81](../debugger/includes/win81_md.md)]是开发[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]应用所必需的。

- 扩展 SDK 是扩展平台的可选组件，但不是强制性的为该平台开发应用。

以下各节介绍 SDK 的一般基础结构以及如何创建平台 SDK 和扩展 SDK。

## <a name="platform-sdks"></a>平台 SDK

平台 SDK 需要为平台开发应用。 例如，SDK[!INCLUDE[win81](../debugger/includes/win81_md.md)]需要为[!INCLUDE[win81](../debugger/includes/win81_md.md)]开发应用。

### <a name="installation"></a>安装

所有平台 SDK 都将安装在*HKLM_软件\微软\\SDK [TPI][tPV]\\ @InstallationFolder [ SDK 根]*。 因此，SDK[!INCLUDE[win81](../debugger/includes/win81_md.md)]安装在*HKLM_软件\微软 SDK_Windows_v8.1*。

### <a name="layout"></a>布局

平台 SDK 具有以下布局：

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

| 节点 | 描述 |
|------------------------| - |
| *引用*文件夹 | 包含可以编码的 API 的二进制文件。 这些可能包括 Windows 元数据 （WinMD） 文件或程序集。 |
| *设计时间*文件夹 | 包含仅在运行/调试前需要的文件。 这些可能包括 XML 文档、库、标头、工具箱设计时间二进制文件、MSBuild 项目等<br /><br /> 理想情况下，XML 文档将放置在 *_DesignTime*文件夹中，但引用的 XML 文档将继续与 Visual Studio 中的参考文件一起放置。 例如，引用的XML文档<em>[\\参考 ]config]\\[arch]_sample.dll</em>将为 *[参考\\]config]\\[arch_c_c.xml），* 该文档的本地化版本将为 *[\\参考 ]config]\\\\[arch] [locale]_sample.xml*。 |
| *配置*文件夹 | 只能有三个文件夹：*调试*、*零售*和*通用配置*。 如果应使用同一组 SDK 文件，SDK 作者可以将其文件置于 *"通用配置"* 下，而不管 SDK 使用者将针对哪个配置。 |
| *体系结构*文件夹 | 任何支持的*体系结构*文件夹都可以存在。 Visual Studio 支持以下体系结构：x86、x64、ARM 和中性。 注意：Win32 映射到 x86，AnyCPU 映射到中性。<br /><br /> MSBuild 仅在平台 SDK 的 *[通用配置]中性*下查找。 |
| *SDKManifest.xml* | 此文件描述可视化工作室应如何使用 SDK。 查看 SDK 清单： [!INCLUDE[win81](../debugger/includes/win81_md.md)]<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **显示名称：** 对象浏览器在"浏览"列表中显示的值。<br /><br /> **平台标识：** 此属性的存在告诉 Visual Studio 和 MSBuild SDK 是一个平台 SDK，并且从它添加的引用不应在本地复制。<br /><br /> **目标框架：** Visual Studio 使用此属性来确保只有针对此属性值中指定的相同框架的项目才能使用 SDK。<br /><br /> **最小VSVersion：** Visual Studio 使用此属性仅使用应用于它的 SDK。<br /><br /> **参考：** 必须仅为包含控件的引用指定此属性。 有关如何指定引用是否包含控件的信息，请参阅下文。 |

## <a name="extension-sdks"></a>扩展 SDK

以下各节介绍部署扩展 SDK 需要执行哪些操作。

### <a name="installation"></a>安装

可以为特定用户或所有用户安装扩展 SDK，而无需指定注册表项。 要为所有用户安装 SDK，请使用以下路径：

*%程序文件%\微软 SDK\<目标平台\>\v<平台\>版本号 \扩展 Sdk*

对于特定于用户的安装，请使用以下路径：

*%USERPROFILE%*AppData_本地_微软 SDK\<目标平台\>\v<平台\>版本号 \扩展 Sdk*

如果要使用其他位置，必须执行两项操作之一：

1. 在注册表项中指定它：

     **HKLM_软件\<_微软SDK目标平台>\v<平台版本号\>[扩展SDK\<名称>\<SDKversion>**\

     并添加值为 的`<path to SDK><SDKName><SDKVersion>`（默认）子键。

2. 将 MSBuild`SDKReferenceDirectoryRoot`属性添加到项目文件中。 此属性的值是要引用的扩展 SDK 驻留的目录的分号分隔列表。

### <a name="installation-layout"></a>安装布局

扩展 SDK 具有以下安装布局：

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

1. \\<SDKName\> \\<\>SDKVersion： 扩展 SDK 的名称和版本派生自 SDK 根路径中的相应文件夹名称。 MSBuild 使用此标识在磁盘上查找 SDK，Visual Studio 将在 **"属性"** 窗口和**参考管理器**对话框中显示此标识。

2. *引用*文件夹：包含 API 的二进制文件。 这些可能是 Windows 元数据 （WinMD） 文件或程序集。

3. *Redist*文件夹：运行时/调试所需的文件，应打包为用户应用程序的一部分。 所有二进制文件应放置在 *[redist\\<配置\>\\<拱门\>* 下， 二进制名称应具有以下格式，以确保唯一性： *]*\<公司>。\<产品>。\<目的>。\<扩展><em>。例如，[微软.Cpp.Build.dll。</em> 所有名称可能与其他 SDK 的文件名（例如 javascript、css、pri、xaml、png 和 jpg 文件）冲突的文件都应放置在<em>[redist\\<配置\>\\\>\\<arch<sdkname\>\*下，但与 XAML 控件关联的文件除外。这些文件应放置在 [redist<\\\>\\配置<拱形\>\\<组件名称\></em>下。

4. *DesignTime*文件夹：仅在运行/调试前需要的文件，不应打包为用户应用程序的一部分。 这些可以是 XML 文档、库、标头、工具箱设计时间二进制文件、MSBuild 工件等。 任何供本机项目使用的 SDK 都必须具有*SDKName.props*文件。 下面显示了这种类型的文件的示例。

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

    XML 引用文档放在引用文件旁边。 例如 *，_\\参考<配置\>\\<arch\>_sample.dll*程序集的 XML 引用文档是 *_参考\\<\>\\配置<\>arch _sample.xml，* 并且该文档的本地化版本是*\\_reference<<\> \\<区域\>设置 _sample.xml\>\\*的配置。

5. *配置*文件夹：三个子文件夹：*调试*、*零售*和*通用配置*。 当应使用同一组 SDK 文件时，SDK 作者可以将其文件置于 *"通用配置"* 下，而不管 SDK 使用者所针对的配置如何。

6. *体系结构*文件夹：支持以下体系结构：x86、x64、ARM、中性。 Win32 映射到 x86，AnyCPU 映射到中性。

### <a name="sdkmanifestxml"></a>SDKManifest.xml

*SDKManifest.xml*文件描述了 Visual Studio 应如何使用 SDK。 以下是一个示例：

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

1. 显示名称：显示在 Visual Studio 用户界面中的参考管理器、解决方案资源管理器、对象浏览器和其他位置中的值。

2. 产品名称：整体 SDK 产品名称。 例如[!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)]，SDK 被命名为"Microsoft.WinJS.1.0"和"Microsoft.WinJS.2.0"，它们属于同一个 SDK 产品系列"Microsoft.WinJS"。 此属性允许 Visual Studio 和 MSBuild 进行该连接。 如果此属性不存在，SDK 名称将用作产品系列名称。

3. 框架标识：指定对一个或多个 Windows 组件库的依赖项。 此属性的值将放入使用应用的清单中。 此属性仅适用于 Windows 组件库。

4. 目标框架：指定参考管理器和工具箱中可用的 SDK。 这是目标框架名字的分号分隔列表，例如".NET 框架，版本_v2.0;.NET 框架，版本_v4.5.1"。 如果指定了同一目标框架的多个版本，则参考管理器将使用最低指定版本进行筛选。 例如，如果指定了".NET 框架、版本=v2.0;.NET 框架、版本=v4.5.1"，则参考管理器将使用".NET 框架，版本=v2.0"。 如果指定了特定的目标框架配置文件，则参考管理器将仅使用该配置文件进行筛选。 例如，当指定"银色光，版本=v4.0，配置文件=WindowsPhone"时，参考管理器仅筛选 Windows Phone 配置文件;面向完整 Silverlight 4.0 框架的项目在参考管理器中看不到 SDK。

5. 最小视频工作室版本。

6. MaxPlatformVerson：最大目标平台版本应用于指定扩展 SDK 无法正常工作的平台版本。 例如，Microsoft Visual C++运行时包 v11.0 应仅由 Windows 8 项目引用。 因此，Windows 8 项目的 MaxPlatformVersion 是 8.0。 这意味着参考管理器筛选出适用于 Windows 8.1 项目的 Microsoft Visual C++运行时包，并且 MSBuild 在[!INCLUDE[win81](../debugger/includes/win81_md.md)]项目引用时引发错误。 注意：此元素受支持，在[!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)]中启动。

7. 应用到：通过指定适用的 Visual Studio 项目类型，指定参考管理器中可用的 SDK。 可以识别九个值：WindowsApp 容器、VisualC、VB、CSharp、WindowsXAML、JavaScript、托管和本机。 SDK 作者可以使用 和 （"*"），或 （"&#124;"），而不是 （"！"运算符以精确指定应用于 SDK 的项目类型的范围。

    WindowsApp 容器标识应用的项目[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]。

8. 支持首选32位：支持的值为"True"和"False"。 默认值为"True"。 如果该值设置为"False"，则如果引用 SDK 的项目已[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]启用了"首选32Bit"，则 MSBuild 将返回项目错误（或桌面项目警告）。 有关"首选32Bit"的详细信息，请参阅[生成页、项目设计器 （C#）](../ide/reference/build-page-project-designer-csharp.md)或[编译页、项目设计器（可视化基本版）。](../ide/reference/compile-page-project-designer-visual-basic.md)

9. 支持的体系结构：SDK 支持的体系结构的分号分隔列表。 如果不需要使用项目中的目标 SDK 体系结构，则 MSBuild 将显示一条警告。 如果未指定此属性，MSBuild 永远不会显示这种类型的警告。

10. 支持多个版本：如果此属性设置为**错误**或**警告**，MSBuild 指示同一项目不能引用同一 SDK 系列的多个版本。 如果此属性不存在或设置为 **"允许**"，MSBuild 不会显示这种类型的错误或警告。

11. AppX：指定磁盘上的 Windows 组件库的应用包的路径。 此值在本地调试期间传递到 Windows 组件库的注册组件。 文件名的命名约定是*\<公司>。\<产品>。\<体系结构>。\<配置>。版本\<>.appx*。 配置和体系结构在属性名称和属性值中是可选的，如果它们不适用于 Windows 组件库。 此值仅适用于 Windows 组件库。

12. CopyRedisttoSubDirectory：指定在 *#redist*文件夹下的文件应相对于应用包根目录（即 **"创建应用包"** 向导中选择**的包位置**）和运行时布局根目录复制的位置。 默认位置是应用包和**F5**布局的根。

13. DependsOn：定义此 SDK 所依赖的 SDK 的 SDK 标识列表。 此属性将显示在参考管理器的详细信息窗格中。

14. 更多信息：提供帮助和更多信息的网页 URL。 此值用于参考管理器右侧窗格中的"详细信息"链接。

15. 注册类型：在应用清单中指定 WinMD 注册，并且本机 WinMD 需要注册，该注册具有对应实现 DLL。

16. 文件引用：仅为包含控件或本机 WinMd 的引用指定。 有关如何指定引用是否包含控件的信息，请参阅[在下面指定工具箱项目的位置](#ToolboxItems)。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a>指定工具箱项目的位置

*SDKManifest.xml*架构中的**ToolBoxItems**元素指定平台和扩展 SDK 中工具箱项的类别和位置。 以下示例演示如何指定不同位置。 这适用于 WinMD 或 DLL 参考。

1. 将控件放在工具箱默认类别中。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. 将控件放在特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory= "MyCategoryName"/>
    </File>
    ```

3. 将控件放在特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems VSCategory = "Data">
        <ToolboxItems />
    </File>
    ```

4. 在混合和可视化工作室中将控件放在不同的类别名称下。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. 在混合和可视化工作室中以不同的方式枚举特定控件。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. 枚举特定控件，并将其置于可视化工作室通用路径或仅在"所有控制"组中。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. 枚举特定控件，并在"选择项目"中仅显示特定集，而不在工具箱中。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>请参阅

- [演练：使用C++创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [演练：使用 C# 或可视化基本功能创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [管理项目中的引用](../ide/managing-references-in-a-project.md)
