---
title: 如何：XML 编辑器中执行 XSLT 转换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8085864ebdb73e8233322a2f91a044dec95dc126
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431055"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>如何：在 XML 编辑器中执行 XSLT 转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过“XML 编辑器”可以将 XSLT 样式表与 XML 文档关联，执行转换，以及查看输出。 由 XSLT 转换生成的输出显示在新的文档窗口中。  
  
 **输出**属性指定的输出文件名。 如果**输出**属性为空白，则在临时目录中生成一个文件名。 文件扩展名基于样式表中的 `xsl:output` 元素，可以是 .xml、.txt 或 .htm。  
  
 如果**输出**属性指定的文件名为.htm 或.html 扩展，XSLT 输出预览使用[!INCLUDE[msCoName](../includes/msconame-md.md)]Internet 资源管理器。 所有其他文件扩展名将使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 选择的默认编辑器打开。 例如，如果文件扩展名为 .xml，Visual Studio 将使用“XML 编辑器”。  
  
### <a name="to-execute-an-xslt-transformation-from-an-xml-document"></a>从 XML 文档执行 XSLT 转换  
  
1. 在“XML 编辑器”中打开 XML 文档。  
  
2. 将 XSLT 样式表与 XML 文档关联。  
  
    - 将 `xml-stylesheet` 处理指令添加到 XML 文档中。 例如，将以下行 `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>` 添加到文档序言中。  
  
         或  
  
    - 添加 XSLT 样式表使用**属性**窗口。 在文档中**属性窗口**，单击**浏览**按钮**样式表**字段中，选择 XSLT 样式表，并单击**打开**.  
  
3. 单击**ShowXSL 输出**按钮**XML 编辑器**工具栏。  
  
    > [!NOTE]
    > 如果没有与 XML 文档关联的样式表，对话框会提示您提供要使用的样式表。  
    >   
    >  由 XSLT 转换生成的输出显示在新的文档窗口中。  
  
### <a name="to-execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>从 XSLT 样式表执行 XSLT 转换  
  
1. 在“XML 编辑器”中打开 XSLT 样式表。  
  
2. 指定 XML 文档中的**输入**的文档字段**属性**窗口。  
  
    > [!NOTE]
    > XML 文档是用于转换的输入文档。 如果文档未指定启动 XSLT 转换时，**文件打开**对话框随即出现，并且你可以在该时间在指定文档。  
  
3. 单击**ShowXSLT 输出**按钮**XML 编辑器**工具栏。  
  
     由 XSLT 转换生成的输出显示在新的文档窗口中。  
  
### <a name="to-provide-a-different-output-file-name"></a>提供不同的输出文件名  
  
1. 指定文件的名称在**输出**的文档字段**属性**窗口。  
  
2. 单击**ShowXSLT 输出**按钮**XML 编辑器**工具栏。  
  
     由 XSLT 转换生成的输出显示在新的文档窗口和输出窗口中使用的编辑器上的文件扩展名取决于你**输出**文档属性。  
  
## <a name="see-also"></a>请参阅  
 [XML 编辑器](../xml-tools/xml-editor.md)
