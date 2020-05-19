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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592693"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>如何：通过 XML 编辑器执行 XSLT 转换

通过 XML 编辑器可以将 XSLT 样式表与 XML 文档关联、执行转换以及查看输出。 由 XSLT 转换生成的输出显示在新的文档窗口中。

“输出”属性指定输出的文件名。 如果“输出”属性为空白，则在临时目录中生成一个文件名。 文件扩展名基于样式表中的 `xsl:output` 元素，可以是 .xml、.txt 或 .htm  。

如果“输出”属性指定了扩展名为 .htm 或 .html 的文件名，XSLT 输出将使用 Web 浏览器进行预览 。 所有其他文件扩展名将使用 Visual Studio 选择的默认编辑器打开。 例如，如果文件扩展名为 .xml，Visual Studio 将使用 XML 编辑器。

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>从 XML 文件执行 XSLT 转换

1. 在 XML 编辑器中打开 XML 文档。

2. 将 XSLT 样式表与 XML 文档关联。

    - 将 `xml-stylesheet` 处理指令添加到 XML 文档中。 例如，将以下行添加到文档 prolog 中：`<?xml-stylesheet type='text/xsl' href='filename.xsl'?>`

       \- 或 -

    - 使用“属性”窗口添加 XSLT 样式表。 在编辑器中打开 XML 文件后，右键单击编辑器中的任意位置，然后选择“属性”。 在“属性”窗口中，在“样式表”字段中单击，然后选择浏览按钮 (...)。选择 XSLT 样式表，然后选择“打开”。

3. 在菜单栏上，选择“XML” > “开始 XSLT 而不调试”。 或者按 Ctrl+Alt+F5。

   来自 XSLT 转换的输出显示在新的文档窗口中。

   > [!NOTE]
   > 如果没有与 XML 文档关联的样式表，对话框会提示您提供要使用的样式表。

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>从 XSLT 样式表执行 XSLT 转换

1. 在 XML 编辑器中打开 XSLT 样式表。

2. 在文档“属性”窗口的“输入”字段中指定 XML 文档 。

   > [!NOTE]
   > XML 文档是用于转换的输入文档。 如果在 XSLT 转换开始时未指定文档，“文件打开”对话框将出现，可以在此时指定文档。

3. 在菜单栏上，选择“XML” > “开始 XSLT 而不调试”。 或者按 Ctrl+Alt+F5。

   来自 XSLT 转换的输出显示在新的文档窗口中。

## <a name="specify-an-output-file-name"></a>指定输出文件名

可以指定 XML 和 XSL 文件的输出文件名。 打开“属性”窗口，然后在“输出”字段中指定文件名。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
