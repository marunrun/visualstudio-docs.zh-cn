---
title: XML 文档属性，“属性”窗口
ms.date: 03/05/2019
ms.topic: reference
ms.assetid: 9dbb34d9-02ea-4201-b445-c98a0eb0d6db
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 679ac529708a49d18025672ce8f880c4f7710471
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808127"
---
# <a name="xml-document-properties-properties-window"></a>XML 文档属性，属性窗口

**属性**窗口提供了有关的文档的 XML 编辑器中处于活动状态的基本信息。 可用的属性取决于当前的活动 XML 文档的类型。

> [!NOTE]
> 所有 XML 文档属性均保存在该解决方案中。 因此，下次打开该解决方案时，不必重新输入这些值。

**编码**

文件的字符编码。 更改此属性将同时更改 XML 声明的编码属性，反之亦然。 将文件编码保存文件时，使用的新编码。

**输入**

与 XSLT 样式表关联的输入文档。 它由**启动 XSLT**命令，例如， **XML** > **启动但不调试的 XSLT**。 可以使用浏览选择文档 (**...**) 按钮。

在编辑器中打开 XSLT 文件时，会显示此属性。

**输出**

转换 XML 文档时生成的文件。

如果未指定文件，默认文件名称根据生成`method`特性，可以在`xsl:output`元素，它确定文件的扩展名。 默认的文件位于当前用户的临时目录。

**架构**

用于验证的架构。 此按钮将打开**XSD 架构**对话框中，可用于选择要使用的架构。

也可以输入架构的路径。 如果指定了多个架构，每个架构路径必须加双引号。

**Stylesheet**

用于转换文档的 XSLT 文件时**启动 XSLT 调试**并**启动但不调试的 XSLT**使用命令。 如果此字段为空白，编辑器将使用中提供的值`xml-stylesheet`处理指令的文档，或者提示你输入文件名。

在编辑 XSLT 文件时，可以使用此属性指定应是不同的样式表时使用**启动 XSLT 调试**或**启动但不调试的 XSLT**选择命令。 例如，可能想要执行此操作时你正在编辑的样式表，包含在父样式表。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)