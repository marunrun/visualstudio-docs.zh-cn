---
title: 将 XML 数据读入数据集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c34fb87c02ff60d9b28c43130d6fbf3a12e70349
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652895"
---
# <a name="read-xml-data-into-a-dataset"></a>将 XML 数据读入到数据集中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ADO.NET 提供了用于处理 XML 数据的简单方法。 在本演练中，将创建一个 Windows 应用程序，用于将 XML 数据加载到数据集。 然后，该数据集将显示在 <xref:System.Windows.Forms.DataGridView> 控件中。 最后，将在文本框中显示基于 XML 文件内容的 XML 架构。

 本演练由五个主要步骤组成：

1. 创建新项目

2. 创建要读入数据集的 XML 文件

3. 创建用户界面

4. 创建数据集，读取 XML 文件，并将其显示在 <xref:System.Windows.Forms.DataGridView> 控件中

5. 添加代码以根据 <xref:System.Windows.Forms.TextBox> 控件中的 XML 文件显示 XML 架构

> [!NOTE]
> 您看到的对话框和菜单命令可能与 "帮助" 中的描述不同，具体取决于您的当前设置或您使用的版本。 若要更改设置，请在 "**工具**" 菜单上选择 "**导入和导出设置**"。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，你将创建一个包含C#本演练的 Visual Basic 或视觉对象。

#### <a name="to-create-the-new-windows-project"></a>创建新的 Windows 项目

1. 在 "**文件**" 菜单上，创建一个新项目。

2. 将项目命名为 `ReadingXML`。

3. 选择 " **Windows 应用程序**"，然后选择 **"确定"** 。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。

     创建**ReadingXML**项目并将其添加到**解决方案资源管理器**。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>生成要读入数据集的 XML 文件
 由于本演练重点介绍如何将 XML 数据读入数据集，因此会提供 XML 文件的内容。

#### <a name="to-create-the-xml-file-that-will-be-read-into-the-dataset"></a>创建将读入数据集的 XML 文件

1. 在 "**项目**" 菜单上，选择 "**添加新项**"。

2. 选择 " **XML 文件**"，将文件命名为 `authors.xml`，然后选择 "**添加**"。

     该 XML 文件将加载到设计器中，并可供编辑。

3. 将以下代码粘贴到 XML 声明下面的编辑器中：

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

4. 在 "**文件**" 菜单上，选择 "**保存创作者 .xml**"。

## <a name="create-the-user-interface"></a>创建用户界面
 此应用程序的用户界面包括以下各项：

- 一个 <xref:System.Windows.Forms.DataGridView> 控件，它将 XML 文件的内容显示为数据。

- 一个 <xref:System.Windows.Forms.TextBox> 控件，该控件显示 XML 文件的 XML 架构。

- 两个 <xref:System.Windows.Forms.Button> 控件。

  - 一个按钮将 XML 文件读取到数据集，并将其显示在 <xref:System.Windows.Forms.DataGridView> 控件中。

  - 第二个按钮从数据集中提取架构，并通过 <xref:System.IO.StringWriter> 在 <xref:System.Windows.Forms.TextBox> 控件中显示该架构。

#### <a name="to-add-controls-to-the-form"></a>向窗体添加控件

1. 在 "设计" 视图中打开 `Form1`。

2. 从 "**工具箱**" 中，将以下控件拖到窗体上：

    - 一 <xref:System.Windows.Forms.DataGridView> 控件

    - 一 <xref:System.Windows.Forms.TextBox> 控件

    - 两个 <xref:System.Windows.Forms.Button> 控件

3. 设置以下属性：

    |控件|Property|设置|
    |-------------|--------------|-------------|
    |`TextBox1`|**多行**|`true`|
    ||**ScrollBars**|**垂直**|
    |`Button1`|**名称**|`ReadXmlButton`|
    ||**文本**|`Read XML`|
    |`Button2`|**名称**|`ShowSchemaButton`|
    ||**文本**|`Show Schema`|

## <a name="create-the-dataset-thatreceives-the-xml-data"></a>创建 XML 数据的数据集 thatreceives
 在此步骤中，将创建一个名为 `authors` 的新数据集。 有关数据集的详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

#### <a name="to-create-a-new-dataset-that--receives-the-xml-data"></a>创建接收 XML 数据的新数据集

1. 在**解决方案资源管理器**中，选择 " **Form1**" 的源文件，然后在**解决方案资源管理器**工具栏上选择 "**查看设计器**" 按钮。

2. 从工具箱的 "[数据" 选项卡](../ide/reference/toolbox-data-tab.md)中，将**数据集**拖到**Form1**上。

3. 在 "**添加数据集**" 对话框中，选择 "**非类型化数据集**"，然后选择 **"确定"** 。

     **DataSet1**将添加到组件栏。

4. 在 "**属性**" 窗口中，为 `AuthorsDataSet` 设置 "**名称**" 和 "<xref:System.Data.DataSet.DataSetName%2A> 属性"。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>创建事件处理程序以将 XML 文件读取到数据集
 "**读取 xml** " 按钮将 XML 文件读取到数据集。 然后，它将 <xref:System.Windows.Forms.DataGridView> 控件上的属性设置为将其绑定到数据集。

#### <a name="to-add-code-to-the-readxmlbutton_click-event-handler"></a>向 ReadXmlButton_Click 事件处理程序添加代码

1. 在**解决方案资源管理器**中，选择 " **Form1**"，然后在**解决方案资源管理器**工具栏上选择 "**查看设计器**" 按钮。

2. 选择 "**读取 XML** " 按钮。

     **代码编辑器**将在 `ReadXmlButton_Click` 事件处理程序打开。

3. 在 `ReadXmlButton_Click` 事件处理程序中键入以下代码：

     [!code-csharp[VbRaddataFillingAndExecuting#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#2)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#2)]

4. 在 `ReadXMLButton_Click` 事件处理程序代码中，将 `filepath =` 项更改为正确的路径。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>创建事件处理程序以在文本框中显示架构
 "**显示架构**" 按钮创建一个使用架构填充的 <xref:System.IO.StringWriter> 对象，并显示在 <xref:System.Windows.Forms.TextBox>control 中。

#### <a name="to-add-code-to-the-showschemabutton_click-event-handler"></a>向 ShowSchemaButton_Click 事件处理程序添加代码

1. 在**解决方案资源管理器**中，选择 " **Form1**"，然后选择 "**视图设计器**" 按钮。

2. 选择 "**显示架构**" 按钮。

     **代码编辑器**将在 `ShowSchemaButton_Click` 事件处理程序打开。

3. 在 `ShowSchemaButton_Click` 事件处理程序中键入以下代码。

     [!code-csharp[VbRaddataFillingAndExecuting#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#3)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#3)]

## <a name="test-the-form"></a>测试窗体

你现在可以对窗体进行测试，以确保它按预期方式运行。

1. 选择**F5**以运行应用程序。

2. 选择 "**读取 XML** " 按钮。

     DataGridView 显示 XML 文件的内容。

3. 选择 "**显示架构**" 按钮。

     文本框显示 XML 文件的 XML 架构。

## <a name="next-steps"></a>后续步骤

本演练介绍有关将 XML 文件读取到数据集，以及基于 XML 文件的内容创建架构的基本知识。 下面是你可能需要执行的一些任务：

- 编辑数据集中的数据，并将其作为 XML 写回。 有关更多信息，请参见<xref:System.Data.DataSet.WriteXml%2A>。

- 编辑数据集中的数据，并将数据写入数据库。

## <a name="see-also"></a>请参阅
 [在 Visual studio 中访问数据的](../data-tools/accessing-data-in-visual-studio.md)[数据演练](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)在 Visual Studio 中[准备应用程序以接收数据](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad) [XML 工具](../xml-tools/xml-tools-in-visual-studio.md)
