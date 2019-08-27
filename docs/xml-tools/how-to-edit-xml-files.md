---
title: 如何：编辑 XML 文件
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1bcc560c1e0cabd222da68e98de18d7b8bef6ec6
ms.sourcegitcommit: 0f5f7955076238742f2071d286ad8e896f3a6cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68483410"
---
# <a name="how-to-edit-xml-files"></a>如何：编辑 XML 文件

"XML 编辑器" 是用于 XML 文件的新编辑器。 该编辑器可以用于独立的 XML 文件，也可以用于与 Visual Studio 项目关联的文件。 "XML 编辑器" 与以下文件扩展名关联: *.config*、 *dtd*、 *.xml*、 *.xsd*、 *xdr*、 *.xsl*、 *xslt*和 *.vssettings*。 "XML 编辑器" 还与未注册任何特定编辑器并且包含 XML 或 DTD 内容的任何其他文件类型相关联。

> [!NOTE]
> XHTML 文档由“HTML 编辑器”处理。

若要编辑 XML 文件, 请双击要编辑的文件。

## <a name="add-a-new-xml-file-to-a-project"></a>向项目添加新的 XML 文件

1. 从 "**项目**" 菜单中, 选择 "**添加新项**"。

2. 从 "**模板**" 窗格中选择 " **XML 文件**"。

3. 在 "**名称**" 字段中输入文件名, 然后按 "**添加**"。

   该 XML 文件将添加到项目中, 并在 XML 编辑器中打开。 该文件包含默认的 XML 声明 `<?xml version="1.0" encoding="utf-8" ?>`。

## <a name="add-an-existing-xml-file-to-a-project"></a>向项目中添加现有的 XML 文件

1. 从 "**项目**" 菜单中, 选择 "**添加现有项**"。

   此时将显示 "**添加现有项**" 对话框。

2. 选择 XML 文件, 然后按 "**添加**"。

## <a name="create-a-new-xml-or-xslt-file"></a>创建新的 XML 或 XSLT 文件

1. 从 "**文件**" 菜单中选择 "**新建**"。

   此时将显示 "**新建文件**" 对话框。

2. 选择 " **Xml 文件**" 以创建新的 xml 文件;或者, 选择 " **Xslt 文件**" 以创建新的 xslt 样式表。

3. 单击“打开”。

## <a name="create-an-empty-project-for-xml-files"></a>为 XML 文件创建空项目

::: moniker range="vs-2017"

1. 从 "**文件**" 菜单中选择 "**新建** > **项目**"。

   此时将出现“新建项目”对话框。

2. 选择所选的代码语言, 然后选择 "**空项目 (.NET Framework)** " 模板。

3. 单击 **“确定”** 。

::: moniker-end

::: moniker range=">=vs-2019"

1. 从 "**文件**" 菜单中选择 "**新建** > **项目**"。

2. 在模板搜索框中输入 "**空项目**", 选择 "**空项目 (.NET Framework)** " 模板, 然后单击 "**下一步**"。

3. 单击 **“创建”** 。

::: moniker-end

4. 将 XML 文件添加到项目中。

   "XML 编辑器" 查找你添加到此项目中的架构, 并将其用于在此项目打开时编辑的任何 XML、架构或 XSLT 文件中的验证和 IntelliSense。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
- [XML 文档属性, "属性" 窗口](../xml-tools/xml-document-properties-properties-window.md)
- [如何：从 XML 文档创建 XML 架构](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)