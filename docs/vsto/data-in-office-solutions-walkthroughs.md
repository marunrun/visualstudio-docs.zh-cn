---
title: Office 解决方案演练中的数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], walkthroughs
- walkthroughs [Office development in Visual Studio], data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52b2efa5e5def8214736d648e2b90906fe720dbe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62956025"
---
# <a name="data-in-office-solutions-walkthroughs"></a>Office 解决方案演练中的数据
  下列演练演示了如何将文档级自定义项和 VSTO 外接程序中的数据用于 Microsoft Office Word 和 Microsoft Office Excel。

## <a name="bind-controls-to-data"></a>将控件绑定到数据
- [演练：文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md) 演示如何将 SQL Server 数据库中的单个数据字段绑定到 <xref:Microsoft.Office.Tools.Excel.NamedRange> Excel 文档级自定义项中的。

- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md) 演示如何将 SQL Server 数据库中的表绑定到 <xref:Microsoft.Office.Tools.Excel.ListObject> Excel 文档级自定义项中的。

- [演练： VSTO 外接程序项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md) 演示如何将 SQL Server 数据库中的单个数据字段绑定到 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> WORD VSTO 外接程序中的。

- [演练： VSTO 外接程序项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md) 演示如何将 SQL Server 数据库中的表绑定到 <xref:Microsoft.Office.Tools.Excel.ListObject> EXCEL VSTO 外接程序中的。

- [演练：将数据绑定到 Excel 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md) 演示如何将绑定到数据源的控件添加到 Excel 中的操作窗格。

- [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md) 演示如何将操作窗格上的控件绑定到数据。 控件演示 SQL Server 数据库中表之间的主/从关系。

- [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md) 演示如何将 Word 文档中的内容控件绑定到文档中存储的 XML 数据。

## <a name="cache-data-in-document-level-solutions"></a>缓存文档级解决方案中的数据
- [演练：使用缓存的数据集创建主/从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md) 演示如何在工作表上创建主/从关系以及缓存数据，以便可以脱机使用该解决方案。

- [演练：将数据插入到服务器上的工作簿](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md) 演示如何将数据插入 Microsoft Office Excel 工作簿中缓存的数据集，而无需启动 Excel。

- [演练：从服务器上的工作簿中检索缓存的数据](../vsto/walkthrough-retrieving-cached-data-from-a-workbook-on-a-server.md) 演示如何从 Microsoft Office Excel 工作簿中缓存的数据集检索数据而不启动 Excel。

- [演练：更改服务器上的工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md) 演示如何修改在不启动 Excel 的情况下在 Microsoft Office Excel 工作簿中缓存的数据集。

## <a name="see-also"></a>另请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [Office UI 自定义演练](../vsto/office-ui-customization-walkthroughs.md)
- [安全和部署演练](../vsto/security-and-deployment-walkthroughs.md)
- [Office 开发示例](../vsto/office-development-samples.md)
- [开始 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
