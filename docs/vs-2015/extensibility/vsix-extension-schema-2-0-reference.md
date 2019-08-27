---
title: VSIX 扩展架构2.0 引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b63f226b7aaadb851eab95f9b60f88f8f2be5ff1
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68869982"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 扩展架构 2.0 参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSIX 部署清单文件描述 VSIX 包的内容。 文件格式由架构控制。 此架构的版本2.0 支持添加自定义类型和属性。  清单的架构是可扩展的。 清单加载程序将忽略不理解的 XML 元素和属性。

> [!IMPORTANT]
> Visual Studio 2015 可以加载 Visual Studio 2010、Visual Studio 2012 或 Visual Studio 2013 格式的 VSIX 文件。

## <a name="package-manifest-schema"></a>包清单架构
 清单 XML 文件的根元素为`<PackageManifest>`, 其中单个属性`Version`为清单格式的版本。 如果对该格式进行了重大更改, 版本格式将会更改。 本主题介绍清单格式版本 2.0, 该格式是通过将`Version`属性设置为值 version = "2.0" 在清单中指定的。

### <a name="packagemanifest-element"></a>PackageManifest 元素
 `<PackageManifest>`在根元素中, 可以使用以下元素:

- `<Metadata>`-元数据和有关包本身的广告信息。 清单中`Metadata`只允许有一个元素。

- `<Installation>`-此部分定义了可以安装此扩展包的方式, 包括可安装到的应用程序 Sku。 清单中只允许一个元素。`Installation` 清单必须具有`Installation`元素, 否则此包不会安装到任何 SKU。

- `<Dependencies>`-此处定义了此包的依赖项的可选列表。

- `<Assets>`-此部分包含包含在此包中的所有资产。 如果没有此部分, 此包不会显示任何内容。

- `<AnyElement>*`-清单架构的灵活性足以允许任何其他元素。 清单加载程序无法识别的任何子元素都作为额外的 XmlElement 对象在扩展管理器 API 中公开。 使用这些子元素, VSIX 扩展可以在清单文件中定义其他数据, 在 Visual Studio 中运行的代码可在运行时访问。 请参阅[AdditionalElements](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))。

### <a name="metadata-element"></a>Metadata 元素
 本部分是有关包、其标识和广告信息的元数据。 `<Metadata>`包含以下元素:

- `<Identity>`-此项定义此包的标识信息, 并包括以下属性:

  - `Id`–此属性必须是作者所选包的唯一 ID。 该名称应采用与 CLR 类型带命名空间相同的方式:Company.Product.Feature.Name。 `Id`特性限制为100个字符。

  - `Version`–定义此包及其内容的版本。 此属性遵循 CLR 程序集版本控制格式:主要版本. 次要版本. 内部版本. 修订版本 (1.2.40308.00)。 版本号较高的包被视为对包的更新, 并且可以安装在现有的已安装版本上。

  - `Language`–此属性是包的默认语言, 并对应于此清单中的文本数据。 此属性遵循资源程序集的 CLR 区域设置代码约定, 例如 en-us、en、fr。 您可以指定`neutral`来声明将在任何 Visual Studio 版本上运行的非特定语言的扩展。 默认值为 `neutral`。

  - `Publisher`–此属性标识此包的发行者, 无论是公司名称还是单个名称。 `Publisher`特性限制为100个字符。

- `<DisplayName>`-此元素指定在 "扩展管理器" UI 中显示的用户友好包名称。 `DisplayName`内容限制为100个字符。

- `<Description>`-此可选元素是包及其内容的简短说明, 它显示在扩展管理器 UI 中。 `Description`内容可以包含所需的任何文本, 但其长度限制为1000个字符。

- `<MoreInfo>`-此可选元素是指向联机页面的 URL, 其中包含此包的完整说明。 必须将协议指定为 http。

- `<License>`-此可选元素是包含在包中的许可证文件 (.txt, .rtf) 的相对路径。

- `<ReleaseNotes>`-此可选元素是包 (.txt, .rtf) 中包含的发行说明文件的相对路径, 或者是指向显示发行说明的网站的 URL。

- `<Icon>`-此可选元素是包含在包中的图像文件 (png、bmp、jpeg、.ico) 的相对路径。 图标图像应为32x32 像素 (或将收缩到该大小), 并显示在 listview UI 中。 如果未`Icon`指定元素, 则 UI 将使用默认值。

- `<PreviewImage>`-此可选元素是包含在包中的图像文件 (png、bmp、jpeg) 的相对路径。 预览图像应为200x200 大小像素, 并显示在详细信息 UI 中。 如果未`PreviewImage`指定元素, 则 UI 将使用默认值。

- `<Tags>`-此可选元素列出了用于搜索提示的其他以分号分隔的文本标记。 `Tags`元素限制为100个字符。

- `<GettingStartedGuide>`-此可选元素既可以是 HTML 文件的相对路径, 也可以是指向网站的 URL, 其中包含有关如何使用此包内的扩展或内容的信息。 本指南作为安装的一部分启动。

- `<AnyElement>*`-清单架构的灵活性足以允许任何其他元素。 清单加载程序无法识别的任何子元素都将公开为 XmlElement 对象的列表。 使用这些子元素, VSIX 扩展可以在清单文件中定义其他数据, 并在运行时枚举这些数据。

### <a name="installation-element"></a>安装元素
 本部分定义此包的安装方式以及它可以安装到的应用程序 Sku。 本部分包含以下属性:

- `Experimental`–如果你有一个当前为所有用户安装的扩展, 但你正在同一台计算机上开发更新的版本, 则将此特性设置为 true。 例如, 如果你已为所有用户安装了 MyExtension 1.0, 但你想要在同一台计算机上调试 MyExtension 2.0, 请设置实验 = "true"。 此属性在 Visual Studio 2015 Update 1 和更高版本中可用。

- `Scope`–此属性可以采用 "Global" 或 "ProductExtension" 值:

  - "Global" 指定安装的作用域不是特定的 SKU。 例如, 在安装扩展 SDK 时使用此值。

  - "ProductExtension" 指定已安装范围到各个 Visual Studio Sku 的传统 VSIX 扩展 (版本 1.0)。 这是默认值。

- `AllUsers`–此可选特性指定是否将为所有用户安装此包。 默认情况下, 此属性为 "false", 指定包为 "每用户"。 (将此值设置为 "true" 时, 安装用户必须提升到管理权限级别才能安装生成的 VSIX。

- `InstalledByMsi`–此可选特性指定是否由 MSI 安装此包。 MSI 安装的包由 MSI (程序和功能) 安装和管理, 而不是由 Visual Studio 扩展管理器安装。  默认情况下, 此属性为 "false", 指定 MSI 不安装包。

- `SystemComponent`–此可选特性指定是否应将此包视为系统组件。 系统组件未显示在扩展管理器 UI 中, 无法更新。 默认情况下, 此属性为 false, 指定包不是系统组件。

- `AnyAttribute*``Installation` –元素接受一组开放式的特性, 这些特性将在运行时作为名称-值对字典公开。

- `<InstallationTarget>`–此元素控制 VSIX 安装程序安装包的位置。 如果该`Scope`属性的值为 "ProductExtension", 则包必须面向安装了清单文件作为其内容的一部分的 SKU, 以将其可用性播发到扩展。 当特性具有显式或默认值 "ProductExtension" 时, `<InstallationTarget>`元素具有以下特性: `Scope`

  - `Id`–此属性标识包。  属性遵循命名空间约定:Company.Product.Feature.Name。 `Id`属性只能包含字母数字字符, 且限制为100个字符。 预期值:

    - Microsoft.VisualStudio.IntegratedShell

    - Microsoft.VisualStudio.Pro

    - Microsoft.VisualStudio.Premium

    - Microsoft.VisualStudio.Ultimate

    - Microsoft.VisualStudio.VWDExpress

    - Microsoft.VisualStudio.VPDExpress

    - Microsoft.VisualStudio.VSWinExpress

    - Microsoft.VisualStudio.VSLS

    - My.Shell.App

  - `Version`–此属性指定一个版本范围, 其中包含此 SKU 支持的最小和最大版本。 包可以对它支持的 Sku 的版本进行详细说明。 版本范围表示法为 [10.0 – 11.0], 其中

    - [–最低版本 (含)。

    - ] –最高版本 (含)。

    - (-最低版本独占。

    - ) –最高的独占版本。

    - 单个版本 #-仅指定的版本。

    > [!IMPORTANT]
    > Visual Studio 2012 中引入了 VSIX 架构的版本2.0。 若要使用此架构, 必须在计算机上安装 Visual Studio 2012 或更高版本, 并使用该产品中的 VSIXInstaller。 您可以使用 Visual Studio 2012 或更高版本的 Visual studio 的早期版本作为目标, 而只是使用安装程序的更高版本 VSIXInstaller。

  - `AnyAttribute*``<InstallationTarget>` –元素允许在运行时作为名称-值对字典公开的属性集。

### <a name="dependencies-element"></a>依赖项元素
 此元素包含此包声明的依赖项的列表。 如果指定了任何依赖项, 则必须先安装这些`Id`包 (由其标识)。

- `<Dependency>`元素–此子元素具有以下属性:

  - `Id`–此属性必须为依赖包的唯一 ID。 此标识值必须与此`<Metadata><Identity>Id`包所依赖的包的属性相匹配。 `Id`属性遵循命名空间约定:Company.Product.Feature.Name。 属性只能包含字母数字字符, 且限制为100个字符。

  - `Version`–此属性指定一个版本范围, 其中包含此 SKU 支持的最小和最大版本。 包可以对它支持的 Sku 的版本进行详细说明。 版本范围表示法为 [12.0, 13.0], 其中:

    - [–最低版本 (含)。

    - ] –最高版本 (含)。

    - (-最低版本独占。

    - ) –最高的独占版本。

    - 单个版本 #-仅指定的版本。

  - `DisplayName`-此属性是在 UI 元素 (如对话框和错误消息) 中使用的依赖包的显示名称。 除非 MSI 安装了依赖包, 否则属性是可选的。

  - `Location`–此可选特性指定此 VSIX 中的相对路径到嵌套 VSIX 包或依赖项下载位置的 URL。 此属性用于帮助用户查找必备组件包。

  - `AnyAttribute*``Dependency` –元素接受一组开放式的特性, 这些特性将在运行时作为名称-值对字典公开。

### <a name="assets-element"></a>资产元素
 此元素包含此包所`<Asset>`呈现的每个扩展或内容元素的标记列表。

- `<Asset>`-此元素包含以下属性和元素:

  - `Type`–这是此元素表示的扩展或内容类型。 每`<Asset>`个元素必须具有单个`Type`, 但多`<Asset>`个元素可能具有相同`Type`的。 根据命名空间约定, 此特性应表示为完全限定名称。 已知类型为:

    1. Microsoft.VisualStudio.VsPackage

    2. Microsoft.VisualStudio.MefComponent

    3. Microsoft.VisualStudio.ToolboxControl

    4. Microsoft.VisualStudio.Samples

    5. Microsoft.VisualStudio.ProjectTemplate

    6. Microsoft.VisualStudio.ItemTemplate

    7. Microsoft.VisualStudio.Assembly

       您可以创建自己的类型, 并为它们指定唯一名称。 在 Visual Studio 中运行时, 你的代码可以通过扩展管理器 API 枚举和访问这些自定义类型。

  - 路径–包中包含资产的文件或文件夹的相对路径。

  - `AnyAttribute*`–将在运行时作为名称-值对字典公开的一组开放式特性。

     `<AnyElement>*`–允许在`<Asset>`开始标记和结束标记之间使用任何结构化内容。 所有元素都公开为 XmlElement 对象的列表。 VSIX 扩展可以在清单文件中定义特定于结构的类型的元数据, 并在运行时对其进行枚举。

### <a name="sample-manifest"></a>示例清单

```
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
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
