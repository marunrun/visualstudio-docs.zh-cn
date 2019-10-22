---
title: XML 文档属性，"属性" 窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 9dbb34d9-02ea-4201-b445-c98a0eb0d6db
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f620cc2bd189dccf067c6276f760d21cde5cf05e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669521"
---
# <a name="xml-document-properties-properties-window"></a>XML 文档属性，“属性”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

"**属性**" 窗口提供有关在 "XML 编辑器" 中处于活动状态的文档的基本信息。 可用的属性取决于当前的活动 XML 文档的类型。

> [!NOTE]
> 所有 XML 文档属性均保存在该解决方案中。 因此，下次打开该解决方案时，不必重新输入这些值。

 **编码**文件的字符编码。 更改此属性将同时更改 XML 声明的编码属性，反之亦然。 新编码将用于在保存文件时为文件编码。

 **输入**与 XSLT 样式表关联的输入文档。 它由**ShowXSLT Output**命令使用。 可以使用 "浏览" （ **...** ）按钮选择文档。

 只有 XSLT 文件在“编辑器”窗口中当前处于活动状态时，才会显示此属性。

 **输出**转换 XML 文档时生成的文件。

 如果未指定文件，将根据 `method` 元素的 `xsl:output` 属性生成默认的文件名，该属性确定文件的扩展名。 默认的文件位于当前用户的临时目录。

 **架构**要用于验证的架构。 按钮将打开 " **XSD 架构**" 对话框，该对话框可用于选择要使用的架构。

 也可以输入架构的路径。 如果指定了多个架构，每个架构路径必须加双引号。

 **样式表**使用 "**显示 Xslt 输出**" 命令时用于转换文档的 XSLT 文件。 如果使用 "**显示 XSLT 输出**" 命令时此字段为空，则编辑器将使用文档的 `xml-stylesheet` 处理指令中提供的值，否则将提示你输入文件名。

 在编辑 XSLT 文件时，此属性可用于指定当选择 "**显示 Xslt 输出**" 或 "**调试 xslt** " 命令时，应使用不同的样式表。 例如，如果正在编辑的样式表包含在父样式表中，则可能需要这样做。

## <a name="see-also"></a>请参阅
 [Xml 编辑器](../xml-tools/xml-editor.md) [xml 编辑器组件](../xml-tools/xml-editor-components.md)
