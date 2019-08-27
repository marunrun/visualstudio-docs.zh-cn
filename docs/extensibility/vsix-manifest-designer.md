---
title: VSIX 清单设计器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.Sdk.VsixManifestEditor
helpviewer_keywords:
- vsixmanifest
- vsix manifest
- manifest designer
ms.assetid: 5a691e77-cf91-430d-90ea-361d9031ef83
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c13d32ab6b91dce94bab307f6bbc6744f9c17a0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322838"
---
# <a name="vsix-manifest-designer"></a>VSIX 清单设计器
修改 VSIX 包清单文件，这会设置 Visual Studio 扩展的安装行为。

 **VSIX 清单设计器**映射到基础 VSIX 架构。 可以使用相应的控件设计器中设置架构中的每个元素。 有关架构的详细信息，请参阅[VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)。

 若要打开**VSIX 清单设计器**，找到*source.extension.vsixmanifest*文件中**解决方案资源管理器**，并打开该文件。 如果文件不包含有效的 XML，不会打开清单设计器。

> [!NOTE]
> *Source.extension.vsixmanifest*文件输出到*extension.vsixmanifest*生成包时。

## <a name="uielement-list"></a>UIElement 列表
 **VSIX 清单设计器**包含对应于这些架构的顶级元素的四个部分：

- 元数据

- 安装目标

- 资产

- 依赖项

  标题区域包含以下控件。

  **产品名称**介绍扩展插件名称。

  **产品 ID**指定此包的唯一标识信息。

  **作者**指定扩展的作者的名称。

  **版本**指定扩展的版本号。

  **元数据**选项卡包含以下控件。

  **描述**提供的扩展，要在中显示的文本说明**扩展管理器**。

  **语言**指定对应于在清单中的文本数据的包的默认语言。 `Language`属性对于资源程序集，例如，en 遵循公共语言运行时 (CLR) 区域设置代码约定-我们，en，fr-fr 的。 默认情况下，值为非特定语言，这意味着包将在 Visual Studio 的任意语言版本上运行。

  **许可证**指定文本文件，其中包含用户许可协议，如果不存在。

  **图标**指定的图形文件 ( *.png*， *.bmp*， *.jpeg*， *.ico*)，其中包含要在中显示的图标**扩展管理器**，如果存在一个图标。 图标图像必须是 32 x 32 像素或大小调整为那些尺寸。 如果指定无图标，则**扩展管理器**使用默认图标。

  **预览图像**指定的图形文件 ( *.png*， *.bmp*， *.jpeg*， *.ico*) 包含到的预览图像显示在**扩展管理器**、 预览图像是否存在。 预览图像必须是 200 x 200 像素。 如果指定没有预览图像，则**扩展管理器**使用默认映像。

  **标记**添加要用于搜索提示的文本标记。

  **发行说明**指定的文件 ( *.txt*， *.rtf*)，其中包含发行说明。 此外会显示发行说明的网站的 URL。

  **入门指南**指定的文件 ( *.txt*， *.rtf*) 包含有关如何使用 VSIX 包中的扩展插件或内容的信息。 扩展安装完成后，会显示此参考。 此外会显示该指南的网站的 URL。

  **更多信息 URL**指定包含有关该产品的其他信息的网站的 URL。

  **安装目标**选项卡包含以下控件。

  **安装类型**列出了**Visual Studio 扩展**并**扩展 SDK**作为目标类型的安装。 选项有所不同，具体取决于您选择的类型。

  **Visual Studio 扩展**列出了**InstallationTarget**介绍了如何安装此包和到哪些 Visual Studio 产品可以安装此扩展的元素。 每个产品名称和版本或版本范围由单独标识。 可以向列表添加、 修改和删除产品。 名称和产品的版本对应于**Id**并**版本**关联的属性**InstallationTarget**元素。

  **版本范围**是 [12.0，14.0]，并使用以下表示法：

- [-非独占的最低版本

- ] 的非独占的最高版本

- (-独占的最低版本

- ) 的排他的最高版本

- 单个版本 #-指定的版本

  **扩展 SDK**指定并不限于特定产品和版本的全局安装。 **目标平台标识符**是平台，如"Windows"您的目标。 **目标平台版本**是版本，如 8.0，您的目标平台。 **SDK 名称**并**SDK 版本**分别是名称和 SDK 的版本号。

  **此 VSIX 针对所有用户安装 （需要在安装的特权提升）** 如果选中此复选框，为所有用户安装了扩展; 否则，仅为当前用户安装。

  **由 Windows 安装程序安装此 VSIX**如果选中此复选框，Windows 安装程序安装了扩展 ( *.msi*文件); 否则为将其作为典型的 VSIX 包安装 ( *.vsix*文件)。

  **资产**选项卡包含以下控件。

  **列出的资产列表**列出了介绍扩展或内容元素的资产元素，此包图面。 每个扩展插件或内容元素的源、 类型和路径单独列出。 可以向列表添加、 修改和删除扩展和内容的元素。 类型和路径的一个扩展或内容元素对应于`Type`并`Path`关联的属性`Asset`元素。 已知以下类型：

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

  **名称、 源和版本范围**列出了此包的依赖关系元素是此包依赖于其他包。 如果指定的依赖项包，则它必须先安装然后将安装此包;否则，此包必须安装它。

  由标识符、 名称、 版本范围、 源和解析依赖项的方式指定依赖项包。 每个依赖项包的名称、 版本和源单独列出。 可以向列表添加、 修改和删除依赖项包。

  标识符必须匹配`ID`的依赖项包元数据属性。 源可以是当前解决方案、 当前安装的扩展或文件中的项目。 **的依赖关系解析方式**设置可以是嵌套软件包的相对路径或依赖项的下载位置的 URL。 ID、 版本和依赖项包的分辨率对应于`Id`， `Version`，并`Location`属性关联的`Dependency`元素。

## <a name="see-also"></a>请参阅
- [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)
- [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)