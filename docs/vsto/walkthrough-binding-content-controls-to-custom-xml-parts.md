---
title: 演练：将内容控件绑定到自定义 XML 部件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PlainTextContentControl, binding to a custom XML part
- custom XML parts, binding to content controls
- content controls [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], content controls
- DropDownListContentControl, binding items to a custom XML part
- DatePickerContentControl, binding to a custom XML part
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52366cc268335df98da53701e5cde283c67a022d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438707"
---
# <a name="walkthrough-bind-content-controls-to-custom-xml-parts"></a>演练：将内容控件绑定到自定义 XML 部件
  本演练演示如何将对 Word 的文档级自定义项中的内容控件绑定到存储在文档中的 XML 数据。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Word 可以存储 XML 数据，名为*自定义 XML 部件*，在文档中。 可以通过将内容控件绑定到自定义 XML 部件中的元素来控制此数据的显示。 本演练中的示例文档显示了存储在自定义 XML 部件中的员工信息。 打开文档时，内容控件将显示 XML 元素的值。 对内容控件中的文本所进行的任何更改都将保存在自定义 XML 部件中。

 本演练阐释了以下任务：

- 设计时，将内容控件添加到文档级项目的 Word 文档。

- 创建定义元素以绑定到内容控件的 XML 数据文件和 XML 架构。

- 设计时，将 XML 架构附加到文档。

- 将 XML 文件的内容添加到运行时在文档中的自定义 XML 部件。

- 将内容控件绑定到自定义 XML 部件中的元素。

- 将 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 绑定到 XML 架构中定义的值集。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word。

## <a name="create-a-new-word-document-project"></a>创建新的 Word 文档项目
 创建将在本演练中使用的 Word 文档。

### <a name="to-create-a-new-word-document-project"></a>创建新的 Word 文档项目

1. 具有名称创建一个 Word 文档项目**为 employeecontrols**。 创建解决方案的新文档。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 在设计器中打开新的 Word 文档并将添加**为 employeecontrols**投影到**解决方案资源管理器**。

## <a name="add-content-controls-to-the-document"></a>向文档添加内容控件
 创建一个包含三种不同类型的内容控件的表格，其中用户可以查看或编辑有关员工的信息。

### <a name="to-add-content-controls-to-the-document"></a>若要将内容控件添加到文档

1. 在 Word 文档中承载[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]设计器中的，在功能区中，选择**插入**选项卡。

2. 在中**表**组中，选择**表**，并插入包含 2 列和 3 行的表。

3. 在第一列中键入文本，使之类似于以下列：

   ||
   |-|
   |**员工姓名**|
   |**雇佣日期**|
   |**标题**|

4. 在第二个表的列中，选择第一行 (下一步**员工姓名**)。

5. 在功能区中，选择**开发人员**选项卡。

   > [!NOTE]
   > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅[如何：功能区上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

6. 在中**控件**组中，选择**文本**按钮![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl")添加<xref:Microsoft.Office.Tools.Word.PlainTextContentControl>到第一个单元格。

7. 在第二个表的列中，选择第二行 (旁边**雇佣日期**)。

8. 在中**控件**组中，选择**日期选取器**按钮![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl")添加<xref:Microsoft.Office.Tools.Word.DatePickerContentControl>到第二个单元格。

9. 在第二个表的列中，选择第三行 (旁边**标题**)。

10. 在中**控件**组中，选择**下拉列表**按钮![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl")添加<xref:Microsoft.Office.Tools.Word.DropDownListContentControl>到最后一个单元格。

    这是此项目的整个用户界面。 如果现在运行项目，则可以在第一行中键入文本并在第二行选择一个日期。 下一步是将需要显示的数据附加到 XML 文件中的文档。

## <a name="create-the-xml-data-file"></a>创建 XML 数据文件
 通常情况下，你将获取 XML 数据存储在来自外部源（如文件或数据库）的自定义 XML 部件中。 在本演练中，你将创建包含员工数据的 XML 文件，此类数据由将绑定到文档中的内容控件的元素进行标记。 要使数据在运行时可用，则将 XML 文件作为资源嵌入自定义程序集。

#### <a name="to-create-the-data-file"></a>创建数据文件

1. 在 **“项目”** 菜单上选择 **“添加新项”** 。

     “添加新项”  对话框随即出现。

2. 在中**模板**窗格中，选择**XML 文件**。

3. 将文件命名**employees.xml**，然后选择**添加**按钮。

     **Employees.xml**文件将在代码编辑器中打开。

4. 内容替换为**employees.xml**具有以下文本的文件。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <employees xmlns="http://schemas.microsoft.com/vsto/samples">
      <employee>
        <name>Karina Leal</name>
        <hireDate>1999-04-01</hireDate>
        <title>Manager</title>
      </employee>
    </employees>
    ```

5. 在中**解决方案资源管理器**，选择**employees.xml**文件。

6. 在中**属性**窗口中，选择**生成操作**属性，然后将值更改为**嵌入的资源**。

     生成项目时，此步骤将 XML 文件作为资源嵌入程序集。 这使您在运行时的 XML 文件的内容进行访问。

## <a name="create-an-xml-schema"></a>创建 XML 架构
 如果需要将内容控件绑定到自定义 XML 部件中的单个元素，则可以不使用 XML 架构。 但是，要将 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 绑定到值集，则必须创建可以验证前面创建的 XML 数据文件的 XML 架构。 XML 架构将定义 `title` 元素的可能值。 在本演练中，稍后会将 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 绑定到此元素。

#### <a name="to-create-an-xml-schema"></a>若要创建 XML 架构

1. 在 **“项目”** 菜单上选择 **“添加新项”** 。

     “添加新项”  对话框随即出现。

2. 在中**模板**窗格中，选择**XML 架构**。

3. 架构命名**employees.xsd** ，然后选择**添加**按钮。

     架构设计器随即打开。

4. 在中**解决方案资源管理器**，打开快捷菜单**employees.xsd**，然后选择**查看代码**。

5. 内容替换为**employees.xsd**具有以下架构文件。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <xs:schema xmlns="http://schemas.microsoft.com/vsto/samples"
        targetNamespace="http://schemas.microsoft.com/vsto/samples"
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        elementFormDefault="qualified">
      <xs:element name="employees" type="EmployeesType"></xs:element>
      <xs:complexType name="EmployeesType">
        <xs:all>
          <xs:element name="employee" type="EmployeeType"/>
        </xs:all>
      </xs:complexType>
      <xs:complexType name="EmployeeType">
        <xs:sequence>
          <xs:element name="name" type="xs:string" minOccurs="1" maxOccurs="1"/>
          <xs:element name="hireDate" type="xs:date" minOccurs="1" maxOccurs="1"/>
          <xs:element name="title" type="TitleType" minOccurs="1" maxOccurs="1"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="TitleType">
        <xs:restriction base="xs:string">
          <xs:enumeration value ="Engineer"/>
          <xs:enumeration value ="Designer"/>
          <xs:enumeration value ="Manager"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:schema>
    ```

6. 上**文件**菜单上，单击**全部保存**若要保存到所做的更改**employees.xml**并**employees.xsd**文件。

## <a name="attach-the-xml-schema-to-the-document"></a>将 XML 架构附加到文档
 必须将 XML 架构附加到文档以将 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 绑定到 `title` 元素的有效值。

### <a name="to-attach-the-xml-schema-to-the-document--includeword15shortvstoincludesword-15-short-mdmd"></a>若要将 XML 架构附加到文档 ( [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)])

1. 激活**EmployeeControls.docx**在设计器中。

2. 在功能区中，选择**开发人员**选项卡，然后选择**外接程序**按钮。

3. 在中**模板和外接程序**对话框框中，选择**XML 架构**选项卡，然后选择**添加架构**按钮。

4. 浏览到**employees.xsd**架构之前创建的位于项目目录，然后选择**打开**按钮。

5. 选择**确定**按钮**架构设置**对话框。

6. 选择**确定**按钮以关闭**模板和外接程序**对话框。

### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>若要将 XML 架构附加到文档 (Word 2010)

1. 激活**EmployeeControls.docx**在设计器中。

2. 在功能区中，选择**开发人员**选项卡。

3. 在中**XML**组中，选择**架构**按钮。

4. 在中**模板和外接程序**对话框框中，选择**XML 架构**选项卡，然后选择**添加架构**按钮。

5. 浏览到**employees.xsd**架构之前，创建它位于项目目录，然后选择**打开**按钮。

6. 选择**确定**按钮**架构设置**对话框。

7. 选择**确定**按钮以关闭**模板和外接程序**对话框。

     **XML 结构**任务窗格随即打开。

8. 关闭**XML 结构**任务窗格。

## <a name="add-a-custom-xml-part-to-the-document"></a>将自定义 XML 部件添加到文档
 在可以将内容控件绑定到 XML 文件中的元素之前，你必须将 XML 文件的内容添加到文档中的新自定义 XML 部件。

### <a name="to-add-a-custom-xml-part-to-the-document"></a>如要向文档添加自定义 XML 部件

1. 在中**解决方案资源管理器**，打开快捷菜单**ThisDocument.cs**或**ThisDocument.vb**，然后选择**查看代码**。

2. 将以下声明添加到 `ThisDocument` 类。 此代码声明了将自定义 XML 部件添加到对象所用的几个对象。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#1)]

3. 将以下方法添加到 `ThisDocument` 类。 此方法获取作为资源嵌入到程序集中的 XML 数据文件的内容，并以 XML 字符串形式返回该内容。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#3)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#3)]

4. 将以下方法添加到 `ThisDocument` 类。 `AddCustomXmlPart` 方法创建新的自定义 XML 部件，其中包含传递给该方法的 XML 字符串。

     为确保只创建一次自定义 XML 部件，该方法仅在文档中不存在具有匹配 GUID 的自定义 XML 部件时，才会创建自定义 XML 部件。 第一次调用此方法时，该方法将 <xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> 属性的值保存为 `employeeXMLPartID` 字符串。 `employeeXMLPartID` 字符串的值将持久保存在文档中，因为该值是使用 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性声明的。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#4)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#4)]

## <a name="bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>将内容控件绑定到自定义 XML 部件中的元素
 使用将每个内容控件绑定到自定义 XML 部件中的元素**XMLMapping**的每个内容控件的属性。

### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>若要将内容控件绑定到自定义 XML 部件中的元素

1. 将以下方法添加到 `ThisDocument` 类。 此方法将每个内容控件绑定到自定义 XML 部件中的元素，并设置 <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> 的日期显示格式。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#5)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#5)]

## <a name="run-your-code-when-the-document-is-opened"></a>打开文档时运行代码
 创建自定义 XML 部件并在打开文档后将自定义控件绑定到数据。

### <a name="to-run-your-code-when-the-document-is-opened"></a>若要在打开文档后运行代码

1. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法。 此代码获取中的 XML 字符串**employees.xml**文件中，将 XML 字符串添加到在文档中，新的自定义 XML 部件，并将内容控件绑定到自定义 XML 部件中的元素。

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#2)]

## <a name="test-the-project"></a>测试项目
 打开文档后，内容控件将显示自定义 XML 部件中元素的数据。 可以单击<xref:Microsoft.Office.Tools.Word.DropDownListContentControl>若要选择的三个有效值之一`title`中定义的元素**employees.xsd**文件。 如果编辑了任何内容控件中的数据，则新值将保存在文档的自定义 XML 部件中。

### <a name="to-test-the-content-controls"></a>若要测试内容控件

1. 按 F5 运行项目  。

2. 验证文档中的表格类似于下表。 第二列中的每个字符串的均来自文档的自定义 XML 部件中的元素。

    |||
    |-|-|
    |**员工姓名**|**Karina Leal**|
    |**雇佣日期**|**1999 年 4 月 1日日**|
    |**标题**|**Manager**|

3. 选择右侧的单元格**员工姓名**单元格并键入不同的名称。

4. 选择右侧的单元格**雇佣日期**单元格并在日期选取器中选择一个不同的日期。

5. 选择右侧的单元格**标题**单元格并从下拉列表中选择新项。

6. 保存并关闭文档。

7. 在文件资源管理器中打开 *\bin\Debug* 项目位置下的文件夹。

8. 打开快捷菜单**EmployeeControls.docx** ，然后选择**重命名**。

9. 将文件命名**EmployeeControls.docx.zip**。

     **EmployeeControls.docx**以 Open XML 格式保存文档。 通过重命名此文档 *.zip*文件扩展名，可以检查文档的内容。 有关 Open XML 的详细信息，请参阅技术文章[引入了 Office (2007) Open XML 文件格式](/previous-versions/office/developer/office-2007/aa338205(v=office.12))。

10. 打开**EmployeeControls.docx.zip**文件。

11. 打开**customXml**文件夹。

12. 打开快捷菜单**item2.xml** ，然后选择**打开**。

     此文件包含已添加到文档的自定义 XML 部件。

13. 验证 `name`、`hireDate` 和 `title` 元素是否包含输入到文档中的内容控件中的新值。

14. 关闭**item2.xml**文件。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何使用内容控件的更多信息：

- 使用所有可用的内容控件创建模板。 有关详细信息，请参见[演练：使用内容控件创建模板](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)。

- 关闭该文档时修改自定义 XML 部件中的数据。 下次用户打开文档时，绑定到的 XML 元素的内容控件将显示新的数据。

- 使用内容控件保护文档的某些部分。 有关详细信息，请参阅[如何：使用内容控件保护文档的某些部分](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)。

## <a name="see-also"></a>请参阅
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [内容控件](../vsto/content-controls.md)
- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)
- [如何：使用内容控件保护文档的某些部分](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
