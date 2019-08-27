---
title: 读取 XML 数据读入数据集 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 64a5edbec2f9f482981002e609117996f0080e56
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825885"
---
# <a name="read-xml-data-into-a-dataset"></a>将 XML 数据读入到数据集中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ADO.NET 提供了用于处理 XML 数据的简单方法。 在本演练中，您创建的 Windows 应用程序将 XML 数据加载到数据集。 数据集然后显示在<xref:System.Windows.Forms.DataGridView>控件。 最后，在文本框中显示 XML 架构基于 XML 文件的内容。  
  
 本演练包含五个主要步骤：  
  
1. 创建新的项目  
  
2. 创建要读取到数据集的 XML 文件  
  
3. 创建用户界面  
  
4. 创建数据集，读取 XML 文件中，并显示在<xref:System.Windows.Forms.DataGridView>控件  
  
5. 添加代码以显示 XML 架构中的 XML 文件基于<xref:System.Windows.Forms.TextBox>控件  
  
> [!NOTE]
> 对话框和菜单命令，请参阅这些帮助中描述具体取决于您现用的设置或版本可能不同于你正在使用。 若要更改您的设置，在**工具**菜单中，选择**导入和导出设置**。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="create-a-new-project"></a>创建新项目  
 在此步骤中，您可以创建包含本演练中的 Visual Basic 或 Visual C# 项目。  
  
#### <a name="to-create-the-new-windows-project"></a>创建新的 Windows 项目  
  
1. 上**文件**菜单中，创建一个新项目。  
  
2. 将项目命名为 `ReadingXML`。  
  
3. 选择**Windows 应用程序**，然后选择**确定**。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。  
  
     **ReadingXML**创建项目并将其添加到**解决方案资源管理器**。  
  
## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>生成要读取到数据集的 XML 文件  
 由于本演练重点介绍 XML 数据读入数据集，提供的 XML 文件的内容。  
  
#### <a name="to-create-the-xml-file-that-will-be-read-into-the-dataset"></a>若要创建的 XML 文件，将读取到数据集  
  
1. 上**项目**菜单中，选择**添加新项**。  
  
2. 选择**XML 文件**，将文件命名`authors.xml`，然后选择**添加**。  
  
     XML 文件加载到设计器，并可供编辑。  
  
3. 将以下代码粘贴到下面的 XML 声明编辑器：  
  
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
  
#### <a name="to-add-controls-to-the-form"></a>向窗体添加控件  
  
1. 打开`Form1`在设计视图中。  
  
2. 从**工具箱**，将以下控件拖到窗体：  
  
    - 一个<xref:System.Windows.Forms.DataGridView>控件  
  
    - 一个<xref:System.Windows.Forms.TextBox>控件  
  
    - 两个<xref:System.Windows.Forms.Button>控件  
  
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
 在此步骤中，创建名为的新数据集`authors`。 有关数据集的详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。  
  
#### <a name="to-create-a-new-dataset-that--receives-the-xml-data"></a>若要创建新的数据集，它接收 XML 数据  
  
1. 在中**解决方案资源管理器**，选择的源文件**Form1**，然后选择**视图设计器**按钮**解决方案资源管理器**工具栏。  
  
2. 从[工具箱中，数据选项卡](../ide/reference/toolbox-data-tab.md)，拖动**数据集**拖到**Form1**。  
  
3. 在中**添加数据集**对话框中，选择**非类型化数据集**，然后选择**确定**。  
  
     **DataSet1**添加到组件栏。  
  
4. 在中**属性**窗口中，将**名称**并<xref:System.Data.DataSet.DataSetName%2A>属性`AuthorsDataSet`。  
  
## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>创建 XML 文件读入到数据集的事件处理程序  
 **读取 XML**按钮将 XML 文件读取到数据集。 然后设置属性上<xref:System.Windows.Forms.DataGridView>将其绑定到数据集的控件。  
  
#### <a name="to-add-code-to-the-readxmlbuttonclick-event-handler"></a>若要将代码添加到 ReadXmlButton_Click 事件处理程序  
  
1. 在中**解决方案资源管理器**，选择**Form1**，然后选择**视图设计器**按钮**解决方案资源管理器**工具栏。  
  
2. 选择**读取 XML**按钮。  
  
     **代码编辑器**在打开`ReadXmlButton_Click`事件处理程序。  
  
3. 键入下面的代码插入`ReadXmlButton_Click`事件处理程序：  
  
     [!code-csharp[VbRaddataFillingAndExecuting#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#2)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#2)]  
  
4. 在中`ReadXMLButton_Click`事件处理程序代码中，更改`filepath =`进入正确的路径。  
  
## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>创建要在文本框中显示的架构的事件处理程序  
 **显示架构**按钮创建<xref:System.IO.StringWriter>对象的架构填充并显示在<xref:System.Windows.Forms.TextBox>控件。  
  
#### <a name="to-add-code-to-the-showschemabuttonclick-event-handler"></a>若要将代码添加到 ShowSchemaButton_Click 事件处理程序  
  
1. 在中**解决方案资源管理器**，选择**Form1**，然后选择**视图设计器**按钮。  
  
2. 选择**显示架构**按钮。  
  
     **代码编辑器**在打开`ShowSchemaButton_Click`事件处理程序。  
  
3. 键入下面的代码插入`ShowSchemaButton_Click`事件处理程序。  
  
     [!code-csharp[VbRaddataFillingAndExecuting#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#3)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#3)]  
  
## <a name="test-the-form"></a>测试窗体  

现在可以测试窗体，以确保其行为符合预期。
  
1. 选择**F5**运行该应用程序。  
  
2. 选择**读取 XML**按钮。  
  
     DataGridView 显示 XML 文件的内容。  
  
3. 选择**显示架构**按钮。  
  
     在文本框中显示的 XML 文件的 XML 架构。  
  
## <a name="next-steps"></a>后续步骤  

本演练介绍了 XML 文件读取到数据集，以及创建基于 XML 文件的内容架构的基础知识。 下面是一些你可能会在接下来执行的任务：  
  
- 编辑数据集，将它写回以 XML 形式的数据。 有关详细信息，请参阅 <xref:System.Data.DataSet.WriteXml%2A> 。  
  
- 编辑数据集中的数据并将其写出到数据库。
  
## <a name="see-also"></a>请参阅  
 [数据演练](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)   
 [准备应用程序以接收数据](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)
