---
title: 执行 XSLT 转换
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e84b1c6303da4c0db39da1b3585a7d4548560feb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001933"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>如何：通过 XML 编辑器执行 XSLT 转换

XML 编辑器，可将 XSLT 样式表与 XML 文档相关联、 执行转换，并查看输出。 由 XSLT 转换生成的输出显示在新的文档窗口中。

**输出**属性指定的输出文件名。 如果**输出**属性为空白，则在临时目录中生成一个文件名。 基于文件扩展名`xsl:output`元素在样式中的工作表，并可以是。*xml*，。*txt*或。*htm*。

如果**输出**属性指定的文件名。*htm*或。*html*扩展中，XSLT 输出将预览使用 web 浏览器。 使用 Visual studio 选择的默认编辑器打开所有其他文件扩展名。 例如，如果文件扩展名。*xml*，Visual Studio 将使用 XML 编辑器。

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>从 XML 文件中执行 XSLT 转换

1. 在 XML 编辑器中打开 XML 文档。

2. 将 XSLT 样式表与 XML 文档关联。

    - 将 `xml-stylesheet` 处理指令添加到 XML 文档中。 例如，将以下行添加到文档序言中： `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>`

       或

    - 添加 XSLT 样式表使用**属性**窗口。 在编辑器中打开 XML 文件中，右键单击编辑器中的任意位置，然后选择**属性**。 在中**属性**窗口中，在单击**样式表**字段，然后选择浏览按钮 （...）。选择 XSLT 样式表，然后选择**打开**。

3. 在菜单栏上依次选择**XML** > **启动但不调试的 XSLT**。 或者，按**Ctrl**+**Alt**+**F5**。

   在新的文档窗口中显示 XSLT 转换的输出。

   > [!NOTE]
   > 如果没有与 XML 文档关联的样式表，对话框会提示您提供要使用的样式表。

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>从 XSLT 样式表执行 XSLT 转换

1. 在 XML 编辑器中打开 XSLT 样式表。

2. 指定 XML 文档中的**输入**的文档字段**属性**窗口。

   > [!NOTE]
   > XML 文档是用于转换的输入文档。 如果文档未指定启动 XSLT 转换时，**文件打开**会出现对话框，您可以在该时间在指定文档。

3. 在菜单栏上依次选择**XML** > **启动但不调试的 XSLT**。 或者，按**Ctrl**+**Alt**+**F5**。

   在新的文档窗口中显示 XSLT 转换的输出。

## <a name="specify-an-output-file-name"></a>指定输出文件名称

可以指定 XML 和 XSL 文件的输出文件名称。 打开**属性**窗口和文件中指定名称**输出**字段。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)