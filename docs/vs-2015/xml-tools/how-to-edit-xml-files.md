---
title: 如何：编辑 XML 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c099839cda87819ec0ec7932c2b2e6aa7698fa52
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670880"
---
# <a name="how-to-edit-xml-files"></a>如何：编辑 XML 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“XML 编辑器”是 XML 文件的新编辑器。 该编辑器可以用于独立的 XML 文件，也可以用于与 Visual Studio 项目关联的文件。 XML 编辑器与以下文件扩展名关联：.config、.dtd、.xml、.xsd、.xdr、.xsl、.xslt 和 .vssettings。 “XML 编辑器”还与任何其他没有注册特定编辑器并且包含 XML 或 DTD 内容的文件类型关联。

> [!NOTE]
> XHTML 文档由“HTML 编辑器”处理。

### <a name="to-edit-an-xml-file"></a>编辑 XML 文件

1. 双击要编辑的文件。

### <a name="to-add-a-new-xml-file-to-a-project"></a>向项目中添加新的 XML 文件

1. 从 "**项目**" 菜单中，选择 "**添加新项**"。

2. 从 "**模板**" 窗格中选择 " **XML 文件**"。

3. 在 "**名称**" 字段中输入文件名，然后按 "**添加**"。

     该 XML 文件将添加到项目中并在“XML 编辑器”中打开。 该文件包含默认的 XML 声明 `<?xml version="1.0" encoding="utf-8" ?>`。

### <a name="to-add-an-existing-xml-file-to-a-project"></a>向项目中添加现有的 XML 文件

1. 从 "**项目**" 菜单中，选择 "**添加现有项**"。

     此时将显示 "**添加现有项**" 对话框。

2. 选择 XML 文件，然后按 "**添加**"。

### <a name="to-create-a-new-xml-or-xslt-file"></a>新建 XML 或 XSLT 文件

1. 从 "**文件**" 菜单中选择 "**新建**"。

     此时将显示 "**新建文件**" 对话框。

2. 选择 " **Xml 文件**" 以创建新的 xml 文件;或者，选择 " **Xslt 文件**" 以创建新的 xslt 样式表。

3. 单击“打开”。

### <a name="to-create-a-project-for-xml-files"></a>为 XML 文件创建项目

1. 从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

     此时将出现“新建项目”对话框。

2. 选择所选的代码语言，选择 "**空项目**"，然后单击 **"确定"** 。

3. 将 XML 文件添加到项目中。

     “XML 编辑器”找到您添加到此项目中的架构，并在此项目打开时，使用这些架构在您编辑的任何 XML、架构或 XSLT 文件中进行验证和 IntelliSense。

## <a name="see-also"></a>请参阅
 [Xml 编辑器](../xml-tools/xml-editor.md) [xml 文档属性，"属性" 窗口](../xml-tools/xml-document-properties-properties-window.md)[如何：从 xml 文档创建 xml 架构](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)
