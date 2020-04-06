---
title: VSIX 扩展架构 2.0 参考 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78e260c62d67afc10fea25d52169c48b64c82f72
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697905"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 扩展架构 2.0 引用
VSIX 部署清单文件描述 VSIX 包的内容。 文件格式由架构控制。 此架构的版本 2.0 支持添加自定义类型和属性。  清单的架构是可扩展的。 清单加载程序忽略它不理解的XML元素和属性。

> [!IMPORTANT]
> Visual Studio 2015 可在 Visual Studio 2010、Visual Studio 2012 或 Visual Studio 2013 格式中加载 VSIX 文件。

## <a name="package-manifest-schema"></a>包清单架构
 清单XML文件的根元素是`<PackageManifest>`。 它有一个属性`Version`，这是清单格式的版本。 如果对格式进行了重大更改，则版本格式将更改。 本文介绍清单格式版本 2.0，该版本通过在清单中指定，将`Version`属性设置为版本="2.0"的值。

### <a name="packagemanifest-element"></a>包清单元素
 在根`<PackageManifest>`元素中，可以使用以下元素：

- `<Metadata>`- 有关包本身的元数据和广告信息。 清单中`Metadata`只允许一个元素。

- `<Installation>`- 本节定义安装此扩展包的方式，包括它可以安装到的应用程序 SKU。 清单中只允许`Installation`单个元素。 清单必须具有`Installation`元素，否则此包不会安装到任何 SKU 中。

- `<Dependencies>`- 此处定义了此包的可选依赖项列表。

- `<Assets>`- 本节包含此包中包含的所有资产。 如果没有此部分，此包将不会显示任何内容。

- `<AnyElement>*`- 清单架构足够灵活，可以允许任何其他元素。 清单加载程序无法识别的任何子元素在扩展管理器 API 中作为额外的 XmlElement 对象公开。 使用这些子元素，VSIX 扩展可以在清单文件中定义 Visual Studio 中运行的代码在运行时可以访问的其他数据。 请参阅[微软.VisualStudio.扩展管理器.I扩展.附加元素](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))。

### <a name="metadata-element"></a>元数据元素
 本节是关于包、其标识和广告信息的元数据。 `<Metadata>`包含以下元素：

- `<Identity>`- 定义此包的标识信息，并包括以下属性：

  - `Id`- 此属性必须是其作者选择的包的唯一 ID。 名称应与 CLR 类型的名称速度相同：Company.Product.Feature.Name。 该`Id`属性限制为 100 个字符。

  - `Version`- 定义此包的版本及其内容。 此属性遵循 CLR 程序集版本版本格式：主要.Minor.Build.修订版 （1.2.40308.00）。 具有较高版本号的包被视为对包的更新，可以安装在现有已安装的版本上。

  - `Language`- 此属性是包的默认语言，对应于此清单中的文本数据。 此属性遵循资源程序集的 CLR 区域设置代码约定，例如：en-us、en、fr-fr。 您可以指定`neutral`声明将在 Visual Studio 的任何版本上运行的语言中立扩展。 默认值为 `neutral`。

  - `Publisher`- 此属性标识此包的发布者，无论是公司还是个人名称。 该`Publisher`属性限制为 100 个字符。

- `<DisplayName>`- 此元素指定在扩展管理器 UI 中显示的用户友好包名称。 内容`DisplayName`限制为 50 个字符。

- `<Description>`- 此可选元素是扩展管理器 UI 中显示的包及其内容的简短说明。 内容`Description`可以包含所需的任何文本，但仅限于 1000 个字符。

- `<MoreInfo>`- 此可选元素是联机页面的 URL，其中包含此包的完整说明。 协议必须指定为 http。

- `<License>`- 此可选元素是包中包含的许可证文件 （.txt， .rtf） 的相对路径。

- `<ReleaseNotes>`- 此可选元素是包中包含的发行说明文件（.txt，.rtf）的相对路径，或者是显示发行说明的网站的 URL。

- `<Icon>`- 此可选元素是包中包含的图像文件（png、bmp、jpeg、ico）的相对路径。 图标图像应为 32x32 像素（或将缩小到该大小），并显示在列表视图 UI 中。 如果未`Icon`指定任何元素，UI 将使用默认值。

- `<PreviewImage>`- 此可选元素是包中包含的图像文件（png、bmp、jpeg）的相对路径。 预览图像应为 200x200 像素，并显示在详细信息 UI 中。 如果未`PreviewImage`指定任何元素，UI 将使用默认值。

- `<Tags>`- 此可选元素列出了用于搜索提示的其他分号分隔文本标记。 元素`Tags`限制为 100 个字符。

- `<GettingStartedGuide>`- 此可选元素是指向 HTML 文件的相对路径，或指向包含有关如何使用此包中的扩展名或内容的信息的网站的 URL。 本指南作为安装的一部分启动。

- `<AnyElement>*`- 清单架构足够灵活，可以允许任何其他元素。 清单加载程序无法识别的任何子元素都公开为 XmlElement 对象的列表。 使用这些子元素，VSIX 扩展可以在清单文件中定义其他数据，并在运行时枚举它们。

### <a name="installation-element"></a>安装元素
 本节定义安装此包的方式以及它可以安装到的应用程序 SKU。 本节包含以下属性：

- `Experimental`- 如果当前为所有用户安装了扩展，但正在同一台计算机上开发更新版本，则将此属性设置为 true。 例如，如果您已为所有用户安装了 My 扩展 1.0，但希望在同一台计算机上调试 My 扩展 2.0，请设置"实验"，"true"。 此属性在 Visual Studio 2015 更新 1 及更高版本中可用。

- `Scope`- 此属性可以采用值"全局"或"产品扩展"：

  - "全局"指定安装范围不限定为特定的 SKU。 例如，在安装扩展 SDK 时使用此值。

  - "产品扩展"指定安装扩展到单个 Visual Studio SKU 的传统 VSIX 扩展（版本 1.0）。 这是默认值。

- `AllUsers`- 此可选属性指定是否将为此包安装给所有用户。 默认情况下，此属性为 false，它指定包是每个用户。 （将此值设置为 true 时，安装用户必须提升到管理权限级别才能安装生成的 VSIX。

- `InstalledByMsi`- 此可选属性指定此包是否由 MSI 安装。 MSI 安装的程序包由 MSI（程序和功能）安装和管理，而不是由可视化工作室扩展管理器安装和管理。  默认情况下，此属性为 false，它指定 MSI 未安装包。

- `SystemComponent`- 此可选属性指定是否应将此包视为系统组件。 系统组件不显示在扩展管理器 UI 中，并且无法更新。 默认情况下，此属性为 false，它指定包不是系统组件。

- `AnyAttribute*`-`Installation`元素接受一组不限成员名额的属性，这些属性将在运行时作为名称值对字典公开。

- `<InstallationTarget>`-此元素控制 VSIX 安装程序安装包的位置。 如果`Scope`属性的值是"Product 扩展"，则包必须以 SKU 为目标，SKU 已安装清单文件作为其内容的一部分，以通告其可用性到扩展。 当`<InstallationTarget>`属性具有显式或默认值"产品`Scope`扩展"时，元素具有以下属性：

  - `Id`- 此属性标识包。  该属性遵循命名空间约定：Company.Product.Feature.Name。 该`Id`属性只能包含字母数字字符，并且限制为 100 个字符。 预期值：

    - 微软.VisualStudio.集成外壳

    - Microsoft.VisualStudio.Pro

    - 微软.VisualStudio.高级

    - 微软.VisualStudio.终极

    - 微软.VisualStudio.VWDExpress

    - 微软.VisualStudio.VPDExpress

    - 微软.VisualStudio.VSWinExpress

    - 微软.VisualStudio.VSLS

    - 我的.Shell.应用程序

  - `Version`- 此属性指定具有此 SKU 的最小和最大受支持版本的版本范围。 包可以详细说明它支持的 SKU 版本。 版本范围表示法为 [10.0 - 11.0]，其中

    - [ - 最小版本包括。

    - * - 最大版本（包括）。

    - （- 最小版本独占。

    - ） - 最大版本独占。

    - 单个版本 = - 仅指定版本。

    > [!IMPORTANT]
    > VSIX 架构的版本 2.0 在 Visual Studio 2012 中引入。 要使用此架构，您必须在计算机上安装 Visual Studio 2012 或更高版本，并使用该产品的 VSIXInstaller.exe。 您可以使用 Visual Studio 2012 或更高版本的 VSIX 安装程序定位早期版本的 Visual Studio，但只能通过使用安装程序的更高版本。

    Visual Studio 2017 版本号可在[Visual Studio 版本号和发布日期](../install/visual-studio-build-numbers-and-release-dates.md)中找到。

    当表示 Visual Studio 2017 版本的版本时，次要版本应始终为**0**。 例如，Visual Studio 2017 版本 15.3.26730.0 应表示为 [15.0.26730.0，16.0）。 这仅适用于 Visual Studio 2017 和更高版本号。

  - `AnyAttribute*`-`<InstallationTarget>`该元素允许一组开放式属性，这些属性在运行时作为名称值对字典公开。

### <a name="dependencies-element"></a>依赖项元素
 此元素包含此包声明的依赖项列表。 如果指定了任何依赖项，则这些包（由其`Id`标识）必须以前已安装。

- `<Dependency>`元素 - 此子元素具有以下属性：

  - `Id`- 此属性必须是从属包的唯一 ID。 此标识值必须与此`<Metadata><Identity>Id`包所依赖的包的属性匹配。 该`Id`属性遵循命名空间约定：Company.Product.Feature.Name。 该属性只能包含字母数字字符，并且限制为 100 个字符。

  - `Version`- 此属性指定具有此 SKU 的最小和最大受支持版本的版本范围。 包可以详细说明它支持的 SKU 版本。 版本范围表示法为 [12.0， 13.0]，其中：

    - [ - 最小版本包括。

    - * - 最大版本（包括）。

    - （- 最小版本独占。

    - ） - 最大版本独占。

    - 单个版本 = - 仅指定版本。

  - `DisplayName`- 此属性是从属包的显示名称，用于 UI 元素（如对话框和错误消息）。 除非 MSI 安装从属包，否则该属性是可选的。

  - `Location`- 此可选属性指定此 VSIX 中相对路径到嵌套 VSIX 包或依赖项的下载位置的 URL。 此属性用于帮助用户找到先决条件包。

  - `AnyAttribute*`-`Dependency`元素接受一组不限成员名额的属性，这些属性将在运行时作为名称值对字典公开。

### <a name="assets-element"></a>资产元素
 此元素包含此包显示的每个`<Asset>`扩展或内容元素的标记列表。

- `<Asset>`- 此元素包含以下属性和元素：

  - `Type`- 此元素表示的扩展或内容的类型。 每个`<Asset>`元素必须具有单个`Type`，但多个`<Asset>`元素可能具有相同的`Type`。 根据命名空间约定，此属性应表示为完全限定的名称。 已知类型包括：

    1. 微软.VisualStudio.Vs包

    2. Microsoft.VisualStudio.MefComponent

    3. 微软.VisualStudio.工具箱控制

    4. 微软.VisualStudio.示例

    5. 微软.VisualStudio.项目模板

    6. 微软.VisualStudio.项目模板

    7. 微软.VisualStudio.组装

       您可以创建自己的类型，并为他们提供唯一的名称。 在 Visual Studio 内部运行时，代码可以通过扩展管理器 API 枚举和访问这些自定义类型。

  - `Path`- 包含资产的包中文件或文件夹的相对路径。

  - `TargetVersion`- 给定资产适用的版本范围。 用于将多个版本的资产运送到 Visual Studio 的不同版本。 需要 Visual Studio 2017.3 或更高版本才能生效。

  - `AnyAttribute*`- 一组开放式属性，在运行时作为名称值对字典公开。

    `<AnyElement>*`- 在`<Asset>`开始标记和结束标记之间允许任何结构化内容。 所有元素都公开为 XmlElement 对象的列表。 VSIX 扩展可以在清单文件中定义结构化特定于类型的元数据，并在运行时枚举它们。

### <a name="sample-manifest"></a>示例清单

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
  <Metadata>
    <Identity Id="0000000-0000-0000-0000-000000000000" Version="1.0" Language="en-US" Publisher="Company" />
    <DisplayName>Test Package</DisplayName>
    <Description>Information about my package</Description>
    <MoreInfo>http://www.fabrikam.com/Extension1/</MoreInfo>
    <License>eula.rtf</License>
    <ReleaseNotes>notes.txt</ReleaseNotes>
    <Icon>Images\icon.png</Icon>
    <PreviewImage>Images\preview.png</PreviewImage>
  </Metadata>
  <Installation InstalledByMsi="false" AllUsers="false" SystemComponent="false" Scope="ProductExtension">
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="[11.0, 12.0]" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="[4.5,)" />
    <Dependency Id="Microsoft.VisualStudio.MPF.12.0" DisplayName="Visual Studio MPF 12.0" d:Source="Installed" Version="[12.0]" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.VsPackage" d:Source="Project" d:ProjectName="%CurrentProject%" Path="|%CurrentProject%;PkgdefProjectOutputGroup|" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>请参阅

- [船舶视觉工作室扩展](../extensibility/shipping-visual-studio-extensions.md)
