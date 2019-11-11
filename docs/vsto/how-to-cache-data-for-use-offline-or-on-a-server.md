---
title: 如何：缓存数据以便脱机使用或在服务器上使用
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], server use
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- offline data [Office development in Visual Studio]
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio], offline use
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 551d27cf8d40f2e6e9c996b031fa6c4e0a233355
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189574"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>如何：缓存数据以便脱机使用或在服务器上使用
  您可以标记要缓存在文档中的数据项，使其在脱机时可用。 当文档存储在服务器上时，也可以使用其他代码来处理文档中的数据。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 在代码中声明数据项时，可以将数据项标记为缓存; 如果使用的是 <xref:System.Data.DataSet>，则可以在 "**属性**" 窗口中设置属性来标记要缓存的数据项。 如果要缓存的数据项不是 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable>，请确保它满足在文档中进行缓存的条件。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

> [!NOTE]
> 使用标记为**缓存**和**WithEvents**的 Visual Basic 创建的数据集（包括从 "**数据源**" 窗口或 **"工具箱**" 中拖到 " **CacheInDocument** " 属性设置为 True 的数据集）在缓存中以下划线作为其名称的前缀。 例如，如果创建一个数据集并将其命名为**Customers**，则 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 名称将在缓存中 **_Customers** 。 使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 访问此缓存项时，必须指定 **_Customers**而不是**客户**。

### <a name="to-cache-data-in-the-document-using-code"></a>使用代码在文档中缓存数据

1. 将数据项的公共字段或属性声明为项目中主机项类的成员，例如 Word 项目中的 `ThisDocumen`t 类或 Excel 项目中的 `ThisWorkbook` 类。

2. 将 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 特性应用于成员，以将数据项标记为要存储在文档的数据缓存中。 下面的示例将此特性应用于 <xref:System.Data.DataSet>的字段声明。

     [!code-csharp[Trin_VstcoreDataExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#11)]
     [!code-vb[Trin_VstcoreDataExcel#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#11)]

3. 添加代码以创建数据项的实例，如果适用，则从数据库中加载它。

     仅在第一次创建数据项时加载数据项;此后，缓存将保留在文档中，并且你必须编写其他代码来更新它。

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>使用属性窗口缓存文档中的数据集

1. 使用 Visual Studio 设计器中的工具将数据集添加到项目中，例如，通过使用 "**数据源**" 窗口将数据源添加到项目。

2. 如果还没有数据集，请创建一个实例，并在设计器中选择该实例。

3. 在 "**属性**" 窗口中，将 " **CacheInDocument** " 属性设置为**True**。

     有关详细信息，请参阅[Office 项目中的属性](../vsto/properties-in-office-projects.md)。

4. 在 "**属性**" 窗口中，将 "**修饰符**" 属性设置为 "**公共**" （默认情况下为 "**内部**"）。

## <a name="see-also"></a>请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：以编程方式在 Office 文档中缓存数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/save-data-back-to-the-database.md)
