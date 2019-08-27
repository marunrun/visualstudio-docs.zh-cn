---
title: 如何：将架构映射到 Visual Studio 内部的工作表
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 80a19924aaf4fa0afe8e809006ada7fada0288f3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63428116"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>如何：将架构映射到 Visual Studio 内部的工作表
  在 Visual Studio 中打开工作表时，可以将 XML 架构映射到工作表。 使用 Visual Studio 外部打开工作簿时使用的相同 Microsoft Office Excel 工具。 Office 项目创建相同的对象是否将架构映射到工作表之前或之后创建 Excel 解决方案。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> Excel 解决方案中，不能使用多部分的 XML 架构。

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>若要将 XML 架构映射到 Visual Studio 中的 Excel 工作表

1. 打开在 Visual Studio 中的 Excel 工作簿或模板项目。

2. 单击要将焦点移到设计器中的工作表中。

3. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅[如何：功能区上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在中**XML**组中，单击**源**。

     **XML 源**窗口随即打开。

5. 在中**XML 源**窗口中，单击**XML 映射**。

     **XML 映射**对话框随即打开。

6. 在中**XML 映射**对话框中，单击**添加**。

7. 浏览到您的架构文件，选择它，，然后单击**打开**。

8. 单击 **“确定”**。

     架构以表示**XML 源**窗口。 在项目中，类型化<xref:System.Data.DataSet>基于架构，生成和<xref:System.Windows.Forms.BindingSource>创建。

9. 将元素从拖动**XML 源**到想要创建的相应控件放在工作表中的窗口。

     如果您拖动的非重复架构元素，Office 项目会生成<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>自动绑定到控件<xref:System.Windows.Forms.BindingSource>。

     如果您拖动的重复架构元素，Office 项目会生成<xref:Microsoft.Office.Tools.Excel.ListObject>不会自动绑定到数据源的控件。 有关详细信息，请参阅[XML 架构和数据在文档级自定义项](../vsto/xml-schemas-and-data-in-document-level-customizations.md)。

## <a name="see-also"></a>请参阅
- [如何：将架构映射到 Visual Studio 内部的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [XML 架构和文档级自定义项中的数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
