---
title: XML 文档属性，“属性”窗口
ms.date: 03/05/2019
ms.topic: reference
ms.assetid: 9dbb34d9-02ea-4201-b445-c98a0eb0d6db
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1b21f4435737597136e1ac4a4dd8651decaf4c65
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592420"
---
# <a name="xml-document-properties-properties-window"></a>“属性”窗口 -> XML 文档属性

“属性”窗口提供有关 XML 编辑器中的活动文档的基本信息。 可用的属性取决于当前的活动 XML 文档的类型。

> [!NOTE]
> 所有 XML 文档属性均保存在该解决方案中。 因此，下次打开该解决方案时，不必重新输入这些值。

**编码**

文件的字符编码。 更改此属性将同时更改 XML 声明的编码属性，反之亦然。 新编码用于在保存文件时对文件进行编码。

**输入**

与 XSLT 样式表关联的输入文档。 它由“启动 XSLT”命令使用，例如“XML” > “启动 XSLT (不调试)”  。 可以使用“浏览”(…) 按钮选择文档。

只有 XSLT 文件在编辑器中处于打开状态时，才会显示此属性。

**输出**

转换 XML 文档时生成的文件。

如果未指定文件，将根据 `xsl:output` 元素的 `method` 属性生成默认的文件名，该属性确定文件的扩展名。 默认的文件位于当前用户的临时目录。

**架构**

用于验证的架构。 该按钮打开“XSD 架构”对话框，该对话框可以用于选择要使用的架构。

也可以输入架构的路径。 如果指定了多个架构，每个架构路径必须加双引号。

**样式表**

使用“启动 XSLT 调试”和“启动 XSLT (不调试)”命令时，用于转换文档的 XSLT 文件 。 如果此字段为空白，编辑器将使用文档的 `xml-stylesheet` 处理指令中提供的值，或提示你输入文件名。

在编辑 XSLT 文件时，此属性可以用于指定在选择“启动 XSLT 调试”或“启动 XSLT (不调试)”命令时应使用的不同的样式表 。 例如，如果正在编辑的样式表包含在父样式表中，则可能需要这样做。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
