---
title: 如何：脱机时或者在服务器上缓存数据以供使用
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
ms.openlocfilehash: 510d923d2503aeb6e07859813537c9094fe25b09
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419705"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>如何：脱机时或者在服务器上缓存数据以供使用
  您可以将标记数据项目，在文档中，缓存，以便可脱机。 这还使得数据中的服务器上存储的文档时，其他代码要操作的文档。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可以将标记数据项目，在代码中，声明数据项时或者如果正在使用缓存<xref:System.Data.DataSet>，通过设置属性以**属性**窗口。 如果要缓存不是数据项<xref:System.Data.DataSet>或<xref:System.Data.DataTable>，确保其满足缓存到文档中的条件。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

> [!NOTE]
> 使用 Visual Basic 中标记为创建的数据集**Cached**并**WithEvents** (包括从拖动的数据集**数据源**窗口或**工具箱**具有**CacheInDocument**属性设置为**True**) 具有下划线的缓存中名称的前缀。 例如，如果您创建数据集并将其命名**客户**，则<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>名称将是 **_Customers**缓存中。 当你使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>若要访问此缓存的项，必须指定 **_Customers**而不是**客户**。

### <a name="to-cache-data-in-the-document-using-code"></a>使用代码在文档中的缓存数据

1. 如在项目中，主机项类的成员声明的公共字段或属性的数据项`ThisDocumen`Word 项目中的 t 类或`ThisWorkbook`Excel 项目中的类。

2. 将应用<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>要将标记存储在文档的数据缓存中的数据项的成员的属性。 下面的示例将此属性应用到的字段声明<xref:System.Data.DataSet>。

     [!code-csharp[Trin_VstcoreDataExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#11)]
     [!code-vb[Trin_VstcoreDataExcel#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#11)]

3. 添加代码以创建数据项目的实例，如果适用，若要从数据库加载它。

     首次创建; 时仅加载的数据项目此后，缓存保持与该文档而必须编写其他代码进行更新。

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>若要在文档中的数据集使用缓存的属性窗口

1. 通过将数据源添加到你的项目使用使用 Visual Studio 设计器等工具将数据集添加到项目**数据源**窗口。

2. 如果尚未执行操作有一个，并在设计器中选择的实例，请创建数据集的实例。

3. 在中**属性**窗口中，将**CacheInDocument**属性设置为**True**。

     有关详细信息，请参阅[Office 项目中的属性](../vsto/properties-in-office-projects.md)。

4. 在中**属性**窗口中，将**修饰符**属性设置为**公共**(默认情况下它是**内部**)。

## <a name="see-also"></a>请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：以编程方式缓存中的 Office 文档的数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/saving-data.md)
