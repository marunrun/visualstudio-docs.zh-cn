---
title: 如何：在 XML 编辑器中执行 XSLT 转换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b305d88779603b374e5f95842d7a5271a657268
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666538"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>如何：在 XML 编辑器中执行 XSLT 转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过“XML 编辑器”可以将 XSLT 样式表与 XML 文档关联，执行转换，以及查看输出。 由 XSLT 转换生成的输出显示在新的文档窗口中。

 **Output**属性指定输出的文件名。 如果**Output**属性为空白，则在临时目录中生成文件名。 文件扩展名基于样式表中的 `xsl:output` 元素，可以是 .xml、.txt 或 .htm。

 如果**Output**属性指定的文件名的扩展名为 .htm 或 .html，则使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet EXPLORER 预览 XSLT 输出。 所有其他文件扩展名将使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 选择的默认编辑器打开。 例如，如果文件扩展名为 .xml，Visual Studio 将使用“XML 编辑器”。

### <a name="to-execute-an-xslt-transformation-from-an-xml-document"></a>从 XML 文档执行 XSLT 转换

1. 在“XML 编辑器”中打开 XML 文档。

2. 将 XSLT 样式表与 XML 文档关联。

    - 将 `xml-stylesheet` 处理指令添加到 XML 文档中。 例如，将以下行 `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>` 添加到文档序言中。

         或

    - 使用 "**属性**" 窗口添加 XSLT 样式表。 在文档 "**属性" 窗口**中，单击 "**样式表**" 字段的**浏览**按钮，选择 XSLT 样式表，然后单击 "**打开**"。

3. 单击 " **XML 编辑器**" 工具栏上的 " **ShowXSL 输出**" 按钮。

    > [!NOTE]
    > 如果没有与 XML 文档关联的样式表，对话框会提示您提供要使用的样式表。
    >
    >  由 XSLT 转换生成的输出显示在新的文档窗口中。

### <a name="to-execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>从 XSLT 样式表执行 XSLT 转换

1. 在“XML 编辑器”中打开 XSLT 样式表。

2. 在文档 "**属性**" 窗口的 "**输入**" 字段中指定一个 XML 文档。

    > [!NOTE]
    > XML 文档是用于转换的输入文档。 如果在 XSLT 转换启动时未指定文档，则会出现 "**文件打开**" 对话框，你可以在该时间指定文档。

3. 单击 " **XML 编辑器**" 工具栏上的 " **ShowXSLT 输出**" 按钮。

     由 XSLT 转换生成的输出显示在新的文档窗口中。

### <a name="to-provide-a-different-output-file-name"></a>提供不同的输出文件名

1. 在文档 "**属性**" 窗口的 "**输出**" 字段中指定一个文件名。

2. 单击 " **XML 编辑器**" 工具栏上的 " **ShowXSLT 输出**" 按钮。

     XSLT 转换生成的输出显示在新的文档窗口中，并且在 "输出" 窗口中使用的编辑器依赖于 "**输出**文档" 属性的文件扩展名。

## <a name="see-also"></a>请参阅
 [XML 编辑器](../xml-tools/xml-editor.md)
