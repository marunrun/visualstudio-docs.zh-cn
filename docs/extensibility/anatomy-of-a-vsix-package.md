---
title: VSIX 包的剖析 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a6d3f994c531bd36ab4281c5f0b27e993cd3392
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740089"
---
# <a name="anatomy-of-a-vsix-package"></a>VSIX 包的解析
VSIX 包是一个 *.vsix*文件，其中包含一个或多个 visual studio 扩展，以及 visual studio 用来分类和安装扩展的元数据。 该元数据包含在 VSIX 清单和 *[Content_Types] .xml*文件中。 VSIX 包还可以包含一个或多个*vsixlangpack*文件以提供本地化的设置文本，并可能包含用于安装依赖项的其他 VSIX 包。

 VSIX 包格式遵循开放打包约定（OPC）标准。 该包包含二进制文件和支持文件，以及 *[Content_Types] .xml*文件和 *.vsix*清单文件。 一个 VSIX 包可能包含多个项目的输出，甚至包含多个具有自己的清单的包。

> [!NOTE]
> VSIX 包中包含的文件的名称不能包含空格，也不能包含在统一资源标识符（URI）中保留的字符，如[ \[RFC2396\]](https://www.rfc-editor.org/rfc/rfc2396.txt)中所定义。

## <a name="the-vsix-manifest"></a>VSIX 清单
 VSIX 清单包含有关要安装的扩展的信息，并遵循 VSX 架构。 有关详细信息，请参阅[VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。 有关 VSIX 清单的示例，请参阅[PackageManifest 元素（根元素，VSX 架构）](https://msdn.microsoft.com/library/f8ae42ba-775a-4d2b-976a-f556e147f187)。

 当 VSIX 清单包含在 ^ `extension.vsixmanifest` .vsix * 文件中时，它必须命名为。

## <a name="the-content"></a>内容
 VSIX 包可以包含模板、工具箱项、Vspackage 或 Visual Studio 支持的任何其他类型的扩展。

## <a name="language-packs"></a>语言包
 VSIX 包可能包含一*vsixlangpack*文件，以便在安装过程中提供本地化文本。 有关详细信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="dependencies-and-references"></a>依赖项和引用
 VSIX 包可能包含其他 VSIX 包作为引用。 其他每个包都必须包含其自身的 VSIX 清单。

 如果用户尝试安装具有依赖项的扩展，安装程序将验证是否在用户系统上安装了所需的程序集。 如果未找到所需的程序集，则 "**扩展和更新**" 将显示缺少的程序集的列表。

 如果扩展清单包含一个或多个[引用](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100))元素，则**扩展和更新**会将每个引用的清单与系统上安装的扩展进行比较，并安装所引用的扩展（如果尚未安装）。 如果安装了引用扩展的早期版本，则更新的版本将替换它。

 如果多项目解决方案中的项目包含对同一解决方案中另一个项目的引用，则 VSIX 包将包含该项目的依赖项。 您可以通过单击内部项目的引用来重写此行为，然后在 "**属性**" 窗口中，将 " **VSIX 属性" 中包含的输出组**设置为`BuiltProjectOutputGroup`。

 若要包含来自 VSIX 包中引用的程序集的附属`SatelliteDllsProjectOutputGroup` dll，请将添加到**Vsix 属性中包含的输出组**。

## <a name="installation-location"></a>安装位置
 在安装过程中，**扩展和更新**将在 *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions*下的文件夹中查找 VSIX 包的内容。

 默认情况下，安装仅适用于当前用户，因为 *% LocalAppData%* 是用户特定的目录。 但是，如果将清单的[AllUsers](https://msdn.microsoft.com/library/ac817f50-3276-4ddb-b467-8bbb1432455b)元素设置为`True`，则会在上安装该扩展<em>。\\ </em>VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em> ，将可供计算机的所有用户使用。

## <a name="content_typesxml"></a>[Content_Types] .xml
 *[Content_Types] .xml*文件标识展开的 *.vsix*文件中的文件类型。 Visual Studio 在安装包的过程中使用此文件，但不安装文件本身。 有关此文件的详细信息，请参阅[[Content_types] .xml 文件的结构](the-structure-of-the-content-types-dot-xml-file.md)。

 开放式打包约定（OPC）标准要求 *[Content_Types] .xml*文件。 有关 OPC 的详细信息，请参阅 MSDN 网站上的[opc：用于打包数据的新标准](https://blogs.msdn.microsoft.com/msdnmagazine/2007/08/08/opc-a-new-standard-for-packaging-your-data/)。
