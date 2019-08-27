---
title: 缓存数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], about caching data
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c6e0f6d7fcf9920ddb8861712b7c5f8bf04506fc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939410"
---
# <a name="cache-data"></a>缓存数据
  可以缓存文档级自定义项中的数据对象，以便脱机或而无需打开 Microsoft Office Word 或 Microsoft Office Excel，可以访问的数据。 若要缓存对象，该对象必须满足某些要求的数据类型。 .NET Framework 中的许多常见数据类型满足这些要求，包括<xref:System.String>， <xref:System.Data.DataSet>，和<xref:System.Data.DataTable>。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有两种方法将对象添加到数据缓存：

- 若要生成解决方案时，将对象添加到数据缓存，应用<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>对象声明的属性。 有关详细信息，请参阅[如何：脱机时或者在服务器上缓存数据以供使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 若要以编程方式将对象添加到数据缓存在运行时，使用`StartCaching`方法的主机项，如`ThisDocument`或`ThisWorkbook`类。 有关详细信息，请参阅[如何：以编程方式缓存中的 Office 文档的数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

  将对象添加到数据缓存后，可以访问并修改的缓存的数据，而无需启动 Word 或 Excel。 有关详细信息，请参阅[访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="requirements-for-data-objects-to-be-cached"></a>要缓存的数据对象的要求
 若要缓存在解决方案中的数据对象，该对象必须满足以下要求：

- 是读/写公共字段或属性的主机项，如`ThisDocument`或`ThisWorkbook`类。

- 不是索引器或其他参数化的属性。

  此外，数据对象必须可由序列化<xref:System.Xml.Serialization.XmlSerializer>类，这意味着对象的类型必须具有以下特征：

- 为公共类型。

- 具有公共构造函数不带任何参数。

- 不执行需要额外的安全特权的代码。

- 公开仅读/写公共属性 （将忽略其他属性）。

- 不会公开多维数组 （接受嵌套的数组）。

- 从属性和字段中返回的接口。

- 未实现<xref:System.Collections.IDictionary>如果集合。

  当缓存数据对象[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]对象序列化为 XML 字符串存储在*自定义 XML 部件*文档中。 有关详细信息，请参阅[自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

## <a name="cached-data-size-limits"></a>缓存的数据大小限制
 有一些限制，您可以添加到文档中的数据缓存和数据缓存中的任何单个对象的大小的数据总量。 如果超过这些限制，应用程序可能会意外关闭时将数据保存到数据缓存。

 若要避免这些限制，请遵循以下准则：

- 无法将大于 10 MB 的任何对象添加到数据缓存。

- 未将多个 100 MB 的总数据添加到单个文档中的数据缓存。

  这些是近似的值。 确切的限制取决于多种因素，包括可用的 RAM 和正在运行的进程数。

## <a name="control-the-behavior-of-cached-objects"></a>控制缓存对象的行为
 若要获得更好地控制缓存对象的行为，可以实现<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType>接口上的缓存对象的类型。 例如，可以实现此接口，如果你想要控制当对象已更改时如何通知用户。 有关演示如何实现的代码示例<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType>，请参阅`ControlCollection`类中的动态控件示例的 Excel 和 Word 中的动态控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>保存到受密码保护的文档中的缓存数据的更改
 如果缓存中使用密码保护的文档数据对象，将不保存对缓存数据的更改。 通过重写两种方法，可以将更改保存到缓存的数据。 重写这些方法时保存文档时，暂时删除保护并重新应用保存后也能保护操作已完成。

 有关详细信息，请参阅[如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>将 null 值添加到数据缓存时防止数据丢失
 在将对象添加到数据缓存时，所有缓存的对象必须初始化为非**null**值之前保存并关闭文档。 如果任何缓存的对象具有**null**值时保存和关闭，文档[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]自动将数据缓存中删除所有缓存的对象。

 如果添加的对象**null**值到使用的数据缓存<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>属性在设计时，可以使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类，以初始化缓存的数据对象，然后再打开该文档。 这是你想要初始化而无需 Word 或 Excel 安装，然后由最终用户打开该文档的服务器上的缓存的数据的情况下很有用。 有关详细信息，请参阅[访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="see-also"></a>请参阅
- [如何：脱机时或者在服务器上缓存数据以供使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式缓存中的 Office 文档的数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [演练：创建使用缓存的数据集的主从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)
