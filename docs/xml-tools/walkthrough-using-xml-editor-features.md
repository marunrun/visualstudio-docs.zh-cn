---
title: 演练：使用 XML 编辑器功能
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ea8dc357-2e66-455a-aec2-7ccaccfc9adf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e443cf23b8726161a4252e6cef3b77f5d3c37bb
ms.sourcegitcommit: 3cc73e74921a9ceb622542e0e263abeebc455c00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624199"
---
# <a name="walkthrough-use-xml-editor-features"></a>演练：使用 XML 编辑器功能

此演练中的步骤说明如何新建 XML 文档。 该演练还使用的一些使其非常适合 XML 编写 XML 编辑器的功能。

> [!NOTE]
> 在开始本演练之前, 保存*hireDate.xsd*文件 （本主题中的下面包含） 到本地计算机。

## <a name="to-create-a-new-xml-file-and-associate-it-with-an-xml-schema"></a>若要创建新的 XML 文件并将它与 XML 架构相关联

1. 上**文件**菜单，依次指向**新建**，然后单击**文件**。

2. 选择**XML 文件**中**模板**窗格，然后单击**打开**。

     新文件将在编辑器中打开。 该文件包含默认的 XML 声明 `<?xml version="1.0" encoding="utf-8">`。

3. 在文档属性窗口中，单击浏览按钮 ( **...** ) 上**架构**字段。

     **XSD 架构**显示对话框。

4. 单击 **添加**。

     **打开 XSD 架构**显示对话框。

5. 选择*hireDate.xsd*文件，并单击**打开**。

6. 单击 **“确定”** 。

     现在，XML 架构已与 XML 文档关联。 XML 架构用于验证文档。 智能感知还使用该架构来填充有效元素的成员列表。

## <a name="to-add-data"></a>添加数据

1. 在编辑器窗格中键入 `<`。

     成员列表中显示可能的项：

    - **！-** 添加注释。

    - **!DOCTYPE**添加文档类型。

    - **?** 若要添加的处理指令。

    - **员工**添加根元素。

2. 选择 **&lt;！-** 若要添加注释节点，然后按**Enter**。

     编辑器将插入注释结束标记，并将光标置于开始注释标记和结束注释标记之间。

3. 在键入**测试 XML 文件**。

4. 在新行中，键入`<`，然后选择**员工**从成员列表。

     编辑器将添加 XML 元素的开始部分 `<employee`。 此时，可以在元素中添加属性，也可以键入 `>` 结束开始标记。

5. 键入 `>` 以结束该标记。

6. 编辑器将添加结束标记。 添加的结束标记使用波浪形下划线指示验证错误。 **工具提示**显示消息：**元素 employee 具有不完整的内容。预期 'ID'** 。

7. 类型`<`，然后选择**ID**从成员列表。 然后键入 `>`。

     编辑器将添加 XML 元素 `<ID></ID>` 并将光标置于 ID 开始标记的后面。

8. 类型**abc**。

     **Abc**文本具有波浪形下划线。 **工具提示**显示消息：**ID 元素具有根据其数据类型的无效值**。

9. 右键单击 ID 元素，然后选择**转到定义**。

     在编辑器打开*hireDate.xsd*在新文档窗口中的文件并将光标置于 ID 架构元素定义。

10. 返回到 XML 文件中，并替换**abc**带有文本**123**。

     停留在波浪形下划线和**工具提示**ID 元素值下清除。 **工具提示**employee 结束标记现在显示的消息：**元素 employee 具有不完整的内容。预期雇佣日期**。

11. 将光标置于 ID 结束标记后面，键入`<`，选择**雇佣日期**从成员列表中，然后键入在`>`。

     编辑器将添加 XML 元素 `<hire-date></hire-date>` 并将光标置于 hire-date 开始标记的后面。

12. 在键入**2003年-01-10**的雇佣日期值。

## <a name="to-format-the-xml-document"></a>格式化 XML 文档

- 选择**格式的文档**按钮在 XML 编辑器工具栏上或按**Ctrl**+**E**，**D**。

   ![在 Visual Studio 中的格式 XML 文档按钮](media/format-xml-document.png)

   XML 文档将重新格式化。

## <a name="to-save-the-xml-document"></a>保存 XML 文档

1. 从**文件**菜单中，选择**另存为**。

     **将文件另存为**显示对话框。 默认文件名*XMLFile1*。

2. 输入的文件名称和 XML 文档的位置，然后单击**保存**。

## <a name="hiredatexsd-file"></a>hireDate.xsd 文件

在本演练中使用以下架构文件：

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

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)