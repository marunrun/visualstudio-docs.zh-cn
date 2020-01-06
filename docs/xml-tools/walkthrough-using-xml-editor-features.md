---
title: 演练：使用 XML 编辑器功能
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d2cf35730b70fc8c8bbec392c73b444b6e8e0aaa
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592459"
---
# <a name="walkthrough-use-xml-editor-features"></a>演练：使用 XML 编辑器功能

此演练中的步骤说明如何新建 XML 文档。 本演练还使用 "XML 编辑器" 的某些功能，使其对 XML 创作很有价值。

> [!NOTE]
> 在开始本演练之前，请将*雇佣项 .xsd*文件（包括在本主题中）保存到本地计算机。

## <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>创建新的 XML 文件并将其与 XML 架构关联

1. 在 "**文件**" 菜单上，指向 "**新建**"，然后单击 "**文件**"。

2. 在 "**模板**" 窗格中选择 " **XML 文件**"，然后单击 "**打开**"。

     新文件将在编辑器中打开。 该文件包含默认的 XML 声明 `<?xml version="1.0" encoding="utf-8">`。

3. 在文档 "属性" 窗口中，单击 "**架构**" 字段上的 "浏览" 按钮（ **...** ）。

     将显示 " **XSD 架构**" 对话框。

4. 单击“添加”。

     随即显示 "**打开 XSD 架构**" 对话框。

5. 选择 "*雇佣*日期" 文件并单击 "**打开**"。

6. 单击" **确定**"。

     现在，XML 架构已与 XML 文档关联。 XML 架构用于验证文档。 智能感知还使用该架构来填充有效元素的成员列表。

## <a name="to-add-data"></a>添加数据

1. 在编辑器窗格中键入 `<`。

     成员列表中显示可能的项：

    - **!--** 添加注释。

    - **!DOCTYPE**来添加文档类型。

    - **?** ，用于添加处理指令。

    - **员工**添加根元素。

2. 选择 **&lt;!--** 添加注释节点并按**enter**。

     编辑器将插入注释结束标记，并将光标置于开始注释标记和结束注释标记之间。

3. 键入 "**测试 XML 文件**"。

4. 在新行上，键入 `<`，并从成员列表中选择**employee** 。

     编辑器将添加 XML 元素的开始部分 `<employee`。 此时，可以在元素中添加属性，也可以键入 `>` 结束开始标记。

5. 键入 `>` 以结束该标记。

6. 编辑器将添加结束标记。 添加的结束标记使用波浪形下划线指示验证错误。 **工具提示**将显示消息：**元素 "employee" 的内容不完整。应为 "ID"** 。

7. 键入 `<` 并从成员列表中选择**ID** 。 然后键入 `>`。

     编辑器将添加 XML 元素 `<ID></ID>` 并将光标置于 ID 开始标记的后面。

8. 键入**abc**。

     **Abc**文本具有波浪形下划线。 **工具提示**将显示消息：**根据数据类型，"ID" 元素的值无效**。

9. 右键单击 ID 元素，然后选择 "**转向定义**"。

     编辑器在新的文档窗口中打开 "*雇佣*日期" 文件，并将光标置于 ID 架构元素定义上。

10. 返回到 XML 文件，并将**abc**文本替换为**123**。

     在 ID 元素值下清除波浪下划线和**工具提示**。 Employee 结束标记的**工具提示**现在显示消息：**元素 "employee" 的内容不完整。应为 "雇佣日期"** 。

11. 将光标置于 ID 结束标记后面，在 "`<`中键入" 成员 "列表中的"**雇佣日期**"，然后键入 `>`。

     编辑器将添加 XML 元素 `<hire-date></hire-date>` 并将光标置于 hire-date 开始标记的后面。

12. 键入**2003-01-10**作为雇用日期值。

## <a name="to-format-the-xml-document"></a>格式化 XML 文档

- 选择 "XML 编辑器" 工具栏上的 "**设置文档格式**" 按钮，或按**Ctrl**+**E**，**D**。

   ![Visual Studio 中的 "XML 文档格式" 按钮](media/format-xml-document.png)

   XML 文档将重新格式化。

## <a name="to-save-the-xml-document"></a>保存 XML 文档

1. 从**文件**菜单中选择**另存为**。

     将显示 "**文件另存为**" 对话框。 默认文件名为 *"XMLFile1"* 。

2. 输入 XML 文档的文件名和位置，然后单击 "**保存**"。

## <a name="hiredatexsd-file"></a>雇佣 .xsd 文件

本演练中使用以下架构文件：

```xml
<?xml version="1.0"?>
<xs:schema attributeFormDefault="unqualified"
     elementFormDefault="qualified" targetNamespace="urn:empl-hire"
     xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="employee">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="ID" type="xs:unsignedShort" />
        <xs:element name="hire-date" type="xs:date" />
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## <a name="see-also"></a>另请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
