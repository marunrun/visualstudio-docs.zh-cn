---
title: 将 XML 数据读入到数据集中
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reading XML
- data access [Visual Studio], XML data
- reading files, XML
- data [Visual Studio], reading from XML files
- reading data, XML files
- XML [Visual Studio], reading
- XML documents, reading
- datasets [Visual Basic], reading XML data
ms.assetid: fae72958-0893-47d6-b3dd-9d42418418e4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 573196ebc0a0719cf736f1299eebae4eb6dcdb73
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821931"
---
# <a name="read-xml-data-into-a-dataset"></a>将 XML 数据读入到数据集中

ADO.NET 提供了用于处理 XML 数据的简单方法。 在本演练中，您创建的 Windows 应用程序将 XML 数据加载到数据集。 数据集然后显示在<xref:System.Windows.Forms.DataGridView>控件。 最后，在文本框中显示 XML 架构基于 XML 文件的内容。

## <a name="create-a-new-project"></a>创建新项目

创建一个新**Windows 窗体应用程序**任意一个项目C#或 Visual Basic。 将项目命名**ReadingXML**。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>生成要读取到数据集的 XML 文件

由于本演练重点介绍 XML 数据读入数据集，提供的 XML 文件的内容。

1. 在“项目”菜单上，选择“添加新项”   。

2. 选择**XML 文件**，将文件命名**authors.xml**，然后选择**添加**。

   XML 文件加载到设计器，并可供编辑。

3. 将以下 XML 数据粘贴到编辑器中的 XML 声明如下：

   ```xml
   <Authors_Table>
     <authors>
       <au_id>172-32-1176</au_id>
       <au_lname>White</au_lname>
       <au_fname>Johnson</au_fname>
       <phone>408 496-7223</phone>
       <address>10932 Bigge Rd.</address>
       <city>Menlo Park</city>
       <state>CA</state>
       <zip>94025</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>213-46-8915</au_id>
       <au_lname>Green</au_lname>
       <au_fname>Margie</au_fname>
       <phone>415 986-7020</phone>
       <address>309 63rd St. #411</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94618</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>238-95-7766</au_id>
       <au_lname>Carson</au_lname>
       <au_fname>Cheryl</au_fname>
       <phone>415 548-7723</phone>
       <address>589 Darwin Ln.</address>
       <city>Berkeley</city>
       <state>CA</state>
       <zip>94705</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>267-41-2394</au_id>
       <au_lname>Hunter</au_lname>
       <au_fname>Anne</au_fname>
       <phone>408 286-2428</phone>
       <address>22 Cleveland Av. #14</address>
       <city>San Jose</city>
       <state>CA</state>
       <zip>95128</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>274-80-9391</au_id>
       <au_lname>Straight</au_lname>
       <au_fname>Dean</au_fname>
       <phone>415 834-2919</phone>
       <address>5420 College Av.</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94609</zip>
       <contract>true</contract>
     </authors>
   </Authors_Table>
   ```

4. 上**文件**菜单中，选择**保存 authors.xml**。

## <a name="create-the-user-interface"></a>创建用户界面

此应用程序的用户界面由以下内容组成：

- 一个<xref:System.Windows.Forms.DataGridView>XML 文件的内容显示为数据的控件。

- 一个<xref:System.Windows.Forms.TextBox>控件显示 XML 文件的 XML 架构。

- 两个<xref:System.Windows.Forms.Button>控件。

  - 一个按钮将 XML 文件读取到数据集并将其显示<xref:System.Windows.Forms.DataGridView>控件。

  - 第二个按钮提取架构集中的数据，并通过<xref:System.IO.StringWriter>将其显示在<xref:System.Windows.Forms.TextBox>控件。

### <a name="to-add-controls-to-the-form"></a>向窗体添加控件

1. 打开`Form1`在设计视图中。

2. 从**工具箱**，将以下控件拖到窗体：

    - 一个<xref:System.Windows.Forms.DataGridView>控件

    - 一个<xref:System.Windows.Forms.TextBox>控件

    - 两个<xref:System.Windows.Forms.Button>控件

3. 设置以下属性：

    |控件|属性|设置|
    |-------------|--------------|-------------|
    |`TextBox1`|**多行**|`true`|
    ||**ScrollBars**|**垂直**|
    |`Button1`|**名称**|`ReadXmlButton`|
    ||**文本**|`Read XML`|
    |`Button2`|**名称**|`ShowSchemaButton`|
    ||**文本**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>创建接收 XML 数据的数据集

在此步骤中，创建名为的新数据集`authors`。 有关数据集的详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

1. 在中**解决方案资源管理器**，选择的源文件**Form1**，然后选择**视图设计器**按钮**解决方案资源管理器**工具栏。

2. 从[工具箱中，数据选项卡](../ide/reference/toolbox-data-tab.md)，拖动**数据集**拖到**Form1**。

3. 在中**添加数据集**对话框中，选择**非类型化数据集**，然后选择**确定**。

     **DataSet1**添加到组件栏。

4. 在中**属性**窗口中，将**名称**并<xref:System.Data.DataSet.DataSetName%2A>属性`AuthorsDataSet`。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>创建 XML 文件读入到数据集的事件处理程序

**读取 XML**按钮将 XML 文件读取到数据集。 然后设置属性上<xref:System.Windows.Forms.DataGridView>将其绑定到数据集的控件。

1. 在中**解决方案资源管理器**，选择**Form1**，然后选择**视图设计器**按钮**解决方案资源管理器**工具栏。

2. 选择**读取 XML**按钮。

     **代码编辑器**在打开`ReadXmlButton_Click`事件处理程序。

3. 键入下面的代码插入`ReadXmlButton_Click`事件处理程序：

     [!code-csharp[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_1.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_1.vb)]

4. 在中`ReadXMLButton_Click`事件处理程序代码中，更改`filepath =`进入正确的路径。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>创建要在文本框中显示的架构的事件处理程序

**显示架构**按钮创建<xref:System.IO.StringWriter>对象的架构填充并显示在<xref:System.Windows.Forms.TextBox>控件。

1. 在中**解决方案资源管理器**，选择**Form1**，然后选择**视图设计器**按钮。

2. 选择**显示架构**按钮。

     **代码编辑器**在打开`ShowSchemaButton_Click`事件处理程序。

3. 将下面的代码粘贴到 `ShowSchemaButton_Click` 事件处理程序中。

     [!code-csharp[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_2.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_2.vb)]

## <a name="test-the-form"></a>测试窗体

现在可以测试窗体，以确保其行为符合预期。

1. 选择**F5**运行该应用程序。

2. 选择**读取 XML**按钮。

     DataGridView 显示 XML 文件的内容。

3. 选择**显示架构**按钮。

     在文本框中显示的 XML 文件的 XML 架构。

## <a name="next-steps"></a>后续步骤

本演练介绍了 XML 文件读取到数据集，以及创建基于 XML 文件的内容架构的基础知识。 下面是一些你可能会在接下来执行的任务：

- 编辑数据集，将它写回以 XML 形式的数据。 有关详细信息，请参阅 <xref:System.Data.DataSet.WriteXml%2A>。

- 编辑数据集中的数据并将其写出到数据库。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)
