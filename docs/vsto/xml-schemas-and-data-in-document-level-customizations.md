---
title: XML 架构和文档级自定义项中的数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio]
- schemas [Office development in Visual Studio]
- XML [Office development in Visual Studio], XML schemas
- XML schemas [Office development in Visual Studio], about XML schemas and data
- Office development in Visual Studio, XML
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb8bc9b9d3149112517d893cd3a704826b6d92d1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421694"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>XML 架构和文档级自定义项中的数据
  **重要**设置 Microsoft Word 有关本主题中的信息是提供的以独占方式适合的权益和使用个人和组织用户位于美国州和其领土的外部或使用，或开发运行的程序，在 2010 年 1 月，Microsoft 中删除的特定功能实现的时间之前已由 Microsoft 许可的 Microsoft Word 产品被与 Microsoft Word 中的自定义 XML。 有关 Microsoft Word 此信息可能不读取或使用的个人或组织在美国或其区域使用，或开发在 Microsoft Word 2010 年 1 月 10 日之后，由 Microsoft 已许可的产品运行的程序中;这些产品不将行为与相同产品许可在该日期之前或购买，美国以外的使用许可。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel 和 Microsoft Office Word 提供的功能将架构映射到你的文档。 此功能可以简化导入和导出 XML 数据传入和传出文档。

 Visual Studio 公开的编程模型中的控件作为映射文档级自定义项中的架构元素。 对于 Excel，Visual Studio 添加的控件绑定到数据库、 Web 服务和对象中的数据的支持。 对于 Word 和 Excel 中，Visual Studio 将添加对操作窗格，可以使用与映射架构的文档来创建你的解决方案的增强最终用户体验的支持。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

> [!NOTE]
> Excel 解决方案中，不能使用多部分的 XML 架构。

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>架构附加到 Excel 工作簿时创建的对象
 当将架构附加到工作簿时，Visual Studio 将自动创建多个对象，并将它们添加到你的项目。 这些对象不应删除使用 Visual Studio 工具，因为它们由 Excel 进行管理。 若要删除这些对象，映射的元素的工作表中删除或分离架构通过使用 Excel 工具。

 有两个主要对象：

- XML 架构 （XSD 文件）。 对于工作簿中的每个架构，Visual Studio 将架构添加到项目。 这显示为项目项中扩展名为 XSD**解决方案资源管理器**。

- 类型化 <xref:System.Data.DataSet> 类。 此类是根据架构创建的。 此数据集类是在可见**类视图**。

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>架构元素映射到 Excel 工作表时创建的对象
 当您将映射从一个架构元素**XML 源**任务窗格中的向工作表中，Visual Studio 会自动创建多个对象，并将它们添加到你的项目：

- 控件。 为工作簿中每个映射对象<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>（对于非重复架构元素） 的控件或<xref:Microsoft.Office.Tools.Excel.ListObject>（适用于重复架构元素） 的控件中的编程模型创建。 <xref:Microsoft.Office.Tools.Excel.ListObject>可以仅通过从该工作簿中删除映射和映射的对象中删除控件。 有关控件的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

- BindingSource。 当您创建<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>通过将非重复架构元素映射到工作表中，<xref:System.Windows.Forms.BindingSource>创建并<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件绑定到<xref:System.Windows.Forms.BindingSource>。 必须将绑定<xref:System.Windows.Forms.BindingSource>映射到文档，如类型化的一个实例的架构匹配的数据源的实例<xref:System.Data.DataSet>创建类。 通过设置创建绑定<xref:System.Windows.Forms.BindingSource.DataSource%2A>并<xref:System.Windows.Forms.BindingSource.DataMember%2A>属性中公开**属性**窗口。

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource>没有为创建<xref:Microsoft.Office.Tools.Excel.ListObject>对象。 您必须手动将绑定<xref:Microsoft.Office.Tools.Excel.ListObject>通过设置与数据源<xref:System.Windows.Forms.BindingSource.DataSource%2A>并<xref:System.Windows.Forms.BindingSource.DataMember%2A>中的属性**属性**窗口。

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Office 映射架构和 Visual Studio 数据源窗口
 Office 和 Visual Studio 的映射的架构功能**数据源**窗口可帮助你在以便进行报告或编辑 Excel 工作表上显示数据。 在这两种情况下可以将数据元素拖到 Excel 工作表上。 这两种方法创建数据绑定通过控件<xref:System.Windows.Forms.BindingSource>与数据源，如<xref:System.Data.DataSet>或 web 服务。

> [!NOTE]
> 当重复架构元素映射到工作表时，Visual Studio 将创建<xref:Microsoft.Office.Tools.Excel.ListObject>。 <xref:Microsoft.Office.Tools.Excel.ListObject>通过对数据不会自动绑定<xref:System.Windows.Forms.BindingSource>。 您必须手动将绑定<xref:Microsoft.Office.Tools.Excel.ListObject>通过设置与数据源<xref:System.Windows.Forms.BindingSource.DataSource%2A>并<xref:System.Windows.Forms.BindingSource.DataMember%2A>中的属性**属性**窗口。

 下表显示了一些两个方法之间的差异。

|XML 架构|“数据源”窗口|
|----------------|-------------------------|
|使用 Office 接口。|使用**数据源**Visual Studio 窗口中的。|
|支持导入和导出 XML 文件中的数据的内置 Office 功能。|必须提供导入和导出功能以编程方式。|
|必须编写代码以用数据填充生成的控件。|从添加控件**数据源**窗口已进行填充，以及必要的连接字符串使用数据库服务器时自动生成的代码。|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>架构附加到 Word 文档时的行为
 将架构附加到文档级 Office 项目中使用的 Word 文档时，不会创建数据对象。 但是，当架构元素映射到你的文档时，创建控件。 控件的类型取决于映射; 元素的类型重复元素生成<xref:Microsoft.Office.Tools.Word.XMLNodes>控件和生成的非重复元素<xref:Microsoft.Office.Tools.Word.XMLNode>控件。 有关详细信息，请参阅[XMLNodes 控件](../vsto/xmlnodes-control.md)并[XMLNode 控件](../vsto/xmlnode-control.md)。

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>包含 XML 架构的解决方案的部署
 应创建的安装程序来部署使用映射到文档的 XML 架构的解决方案。 安装程序应在用户的计算机上的架构库中注册该架构。 如果不注册该架构，因为 Word 生成基于用户打开它时在文档中的元素的临时架构仍然有效解决方案。 但是，用户将无法再执行验证或保存用于创建项目的架构。 有关安装程序的详细信息，请参阅[部署应用程序、 服务和组件](../deployment/deploying-applications-services-and-components.md)。

 您还可以将代码添加到你的项目以检查架构是否位于库中的、 已注册。 如果不是这样，可以向用户发出警告。

 [!code-vb[Trin_VstcoreDataWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstcoreDataWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs#1)]

## <a name="see-also"></a>请参阅

- [如何：将架构映射到 Visual Studio 内部的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [如何：将架构映射到 Visual Studio 内部的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
