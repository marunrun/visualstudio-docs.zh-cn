---
title: VSIX 清单设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VS.Sdk.VsixManifestEditor
helpviewer_keywords:
- vsixmanifest
- vsix manifest
- manifest designer
ms.assetid: 5a691e77-cf91-430d-90ea-361d9031ef83
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 450d306718906c3b76bf05982594045e7fd215f0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387573"
---
# <a name="vsix-manifest-designer"></a>VSIX 清单设计器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

修改 VSIX 包清单文件，这会设置 Visual Studio 扩展的安装行为。  
  
 **VSIX 清单设计器**映射到基础 VSIX 架构。 可以使用相应的控件设计器中设置架构中的每个元素。 有关架构的详细信息，请参阅[VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)。  
  
 若要打开**VSIX 清单设计器**，找到在 source.extension.vsixmanifest 文件**解决方案资源管理器**，并打开该文件。 如果文件不包含有效的 XML，将不会打开清单设计器。  
  
> [!NOTE]
> 生成包时，Source.extension.vsixmanifest 被输出到 extension.vsixmanifest。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **VSIX 清单设计器**包含对应于这些架构的顶级元素的四个部分：  
  
- 元数据  
  
- 安装目标  
  
- 资产  
  
- 依赖项  
  
  标题区域包含以下控件。  
  
  **产品名称**  
  介绍了扩展插件名称。  
  
  **产品 ID**  
  指定此包的唯一标识信息。  
  
  **Author**  
  指定扩展的作者的名称。  
  
  **Version**  
  指定扩展的版本号。  
  
  **元数据**选项卡包含以下控件。  
  
  **说明**  
  提供的扩展，要在中显示的文本说明**扩展管理器**。  
  
  **语言**  
  指定了对应于在清单中的文本数据的包的默认语言。 `Language`属性对于资源程序集，例如，en 遵循公共语言运行时 (CLR) 区域设置代码约定-我们，en，fr-fr 的。 默认情况下，值为非特定语言;这意味着在任何语言版本的 Visual Studio 将运行包。  
  
  **许可证**  
  指定的文件，包含用户许可协议，如果不存在。  
  
  **图标**  
  指定包含要在中显示的图标的图形文件 （.png、.bmp、.jpeg、.ico）**扩展管理器**，如果存在一个图标。 图标图像必须是 32 x 32 像素，或者它将调整为那些尺寸。 如果指定无图标，则**扩展管理器**使用默认图标。  
  
  **预览图像**  
  指定包含要在中显示的预览图像的图形文件 （.png、.bmp、.jpeg、.ico）**扩展管理器**、 预览图像是否存在。 预览图像必须是 200 x 200 像素。 如果指定没有预览图像，则**扩展管理器**使用默认映像。  
  
  **标记**  
  添加要用于搜索提示的文本标记。  
  
  **发行说明**  
  指定包含发行说明的文件 （.txt、.rtf）。 此外会显示发行说明的网站的 URL。  
  
  **入门指南**  
  指定包含有关如何在 VSIX 包中使用的扩展插件或内容的信息的文件 （.txt、.rtf）。 扩展安装完成后，会显示此参考。 此外会显示该指南的网站的 URL。  
  
  **详细信息 URL**  
  指定包含有关该产品的其他信息的网站的 URL。  
  
  **安装目标**选项卡包含以下控件。  
  
  **安装类型**  
  列出**Visual Studio 扩展**并**扩展 SDK**作为目标类型的安装。 选项有所不同，具体取决于您选择的类型。  
  
  **Visual Studio 扩展**  
  列出**InstallationTarget**介绍了如何安装此包和到哪些 Visual Studio 产品可以安装此扩展的元素。 每个产品名称和版本或版本范围由单独标识。  可以向列表添加、 修改和删除产品。 名称和产品的版本对应于**Id**并**版本**关联的属性**InstallationTarget**元素。  
  
  **版本范围**是 [12.0，14.0]，并使用以下表示法：  
  
- [-非独占的最低版本  
  
- ] – 非独占的最高版本  
  
- (-独占的最低版本  
  
- ) – 排他的最高版本  
  
- 单个版本 #-指定的版本  
  
  **扩展 SDK**  
  指定不应用范围限定为特定产品和版本的全局安装。 **目标平台标识符**是平台，如"Windows"您的目标。 **目标平台版本**是版本，如 8.0，您的目标平台。 **SDK 名称**并**SDK 版本**分别是名称和 SDK 的版本号。  
  
  **此 VSIX 针对所有用户安装 （需要在安装的特权提升）** 复选框  
  如果选中此复选框，此扩展已安装的所有用户;否则，它是仅为当前用户安装。  
  
  **由 Windows 安装程序安装此 VSIX**复选框  
  如果选中此复选框，此扩展已安装的 Windows Installer （.msi 文件）;否则，它是作为典型的 VSIX 包 （.vsix 文件） 进行安装。  
  
  **资产**选项卡包含以下控件。  
  
  **列出的资产列表**  
  列出了介绍扩展或内容元素的资产元素，此包图面。 每个扩展插件或内容元素的源、 类型和路径单独列出。 可以向列表添加、 修改和删除扩展和内容的元素。 类型和路径的一个扩展或内容元素对应于`Type`并`Path`关联的属性`Asset`元素。 已知以下类型：  
  
- Microsoft.VisualStudio.Package  
  
- Microsoft.VisualStudio.MefComponent  
  
- Microsoft.VisualStudio.ToolboxControl  
  
- Microsoft.VisualStudio.Samples  
  
- Microsoft.VisualStudio.ProjectTemplate  
  
- Microsoft.VisualStudio.ItemTemplate  
  
- Microsoft.VisualStudio.Assembly  
  
- Microsoft.ExtensionSDK  
  
  若要添加或编辑某项资产，必须指定资产类型是否资产属于当前解决方案中的项目或文件在文件系统和项目的名称。 此外可以指定在其中嵌入的文件夹的名称。  
  
  您还可以创建自己的类型，并为其提供唯一名称。  
  
  **依赖项**选项卡包含以下控件。  
  
  **名称、 源和版本范围**  
  列出了此包的依赖关系元素是此包依赖于其他包。 如果指定的依赖项包，则它必须先安装然后将安装此包;否则，此包必须安装它。  
  
  由标识符、 名称、 版本范围、 源和解析依赖项的方式指定依赖项包。 每个依赖项包的名称、 版本和源单独列出。 可以向列表添加、 修改和删除依赖项包。  
  
  标识符必须匹配`ID`的依赖项包元数据属性。 源可以是当前解决方案、 当前安装的扩展或文件中的项目。 **的依赖关系解析方式**设置可以是嵌套软件包的相对路径或依赖项的下载位置的 URL。 ID、 版本和依赖项包的分辨率对应于`Id`， `Version`，并`Location`属性关联的`Dependency`元素。  
  
## <a name="see-also"></a>请参阅  
 [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)   
 [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
