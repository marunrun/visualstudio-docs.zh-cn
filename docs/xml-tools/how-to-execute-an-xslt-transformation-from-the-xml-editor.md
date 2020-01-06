---
title: 执行 XSLT 转换
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3bd26eaadf921d13fc425a91031a39df5a80ea2a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592693"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>如何：在 XML 编辑器中执行 XSLT 转换

使用 XML 编辑器，您可以将 XSLT 样式表与 XML 文档关联，执行转换，然后查看输出。 由 XSLT 转换生成的输出显示在新的文档窗口中。

**Output**属性指定输出的文件名。 如果**Output**属性为空白，则在临时目录中生成文件名。 文件扩展名基于样式表中的 `xsl:output` 元素，可以为。*xml*、。*txt*或。*htm*。

如果**Output**属性指定的文件名为，则为。*htm*或。*html*扩展，将使用 web 浏览器预览 XSLT 输出。 所有其他文件扩展名均使用 Visual Studio 选择的默认编辑器打开。 例如，如果文件扩展名为。*xml*，Visual Studio 会使用 "xml 编辑器"。

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>从 XML 文件执行 XSLT 转换

1. 在 XML 编辑器中打开 XML 文档。

2. 将 XSLT 样式表与 XML 文档关联。

    - 将 `xml-stylesheet` 处理指令添加到 XML 文档中。 例如，将以下行添加到文档 prolog： `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>`

       或

    - 使用 "**属性**" 窗口添加 XSLT 样式表。 在编辑器中打开 XML 文件后，右键单击编辑器中的任意位置，然后选择 "**属性**"。 在 "**属性**" 窗口中，单击 "**样式表**" 字段，然后选择 "浏览" 按钮（...）。选择 XSLT 样式表，然后选择 "**打开**"。

3. 在菜单栏上，选择 " **XML** > " 在**不调试的情况下启动 XSLT**"。 或者按**Ctrl**+**Alt**+**F5**。

   XSLT 转换的输出显示在新的文档窗口中。

   > [!NOTE]
   > 如果没有与 XML 文档关联的样式表，对话框会提示您提供要使用的样式表。

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>从 XSLT 样式表执行 XSLT 转换

1. 在 XML 编辑器中打开 XSLT 样式表。

2. 在文档 "**属性**" 窗口的 "**输入**" 字段中指定一个 XML 文档。

   > [!NOTE]
   > XML 文档是用于转换的输入文档。 如果在 XSLT 转换启动时未指定文档，则会出现 "**文件打开**" 对话框，你可以在该时间指定文档。

3. 在菜单栏上，选择 " **XML** > " 在**不调试的情况下启动 XSLT**"。 或者按**Ctrl**+**Alt**+**F5**。

   XSLT 转换的输出显示在新的文档窗口中。

## <a name="specify-an-output-file-name"></a>指定输出文件名

可以指定 XML 和 XSL 文件的输出文件名。 打开 "**属性**" 窗口，并在 "**输出**" 字段中指定一个文件名。

## <a name="see-also"></a>另请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
