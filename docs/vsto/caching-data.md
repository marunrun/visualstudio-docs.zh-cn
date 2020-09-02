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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62939410"
---
# <a name="cache-data"></a>缓存数据
  可以在文档级自定义项中缓存数据对象，以便可以脱机访问数据，也可以在不打开 Microsoft Office Word 或 Microsoft Office Excel 的情况下访问数据。 若要缓存对象，对象必须具有满足特定要求的数据类型。 .NET Framework 中的许多常见数据类型都满足这些要求，其中包括 <xref:System.String> 、 <xref:System.Data.DataSet> 和 <xref:System.Data.DataTable> 。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可通过两种方法将对象添加到数据缓存：

- 若要在生成解决方案时将对象添加到数据缓存，请将特性应用于 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 对象声明。 有关详细信息，请参阅 [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 若要在运行时以编程方式将对象添加到数据缓存，请使用 `StartCaching` 主机项（如或类）的方法 `ThisDocument` `ThisWorkbook` 。 有关详细信息，请参阅 [如何：以编程方式在 Office 文档中缓存数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

  将对象添加到数据缓存后，可以在不启动 Word 或 Excel 的情况下访问和修改缓存的数据。 有关详细信息，请参阅在 [服务器上访问文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="requirements-for-data-objects-to-be-cached"></a>要缓存的数据对象的要求
 若要在解决方案中缓存数据对象，对象必须满足以下要求：

- 是主机项（如或类）的读/写公共字段或属性 `ThisDocument` `ThisWorkbook` 。

- 不是索引器或其他参数化属性。

  此外，数据对象必须可由类进行序列化 <xref:System.Xml.Serialization.XmlSerializer> ，这意味着对象的类型必须具有以下特征：

- 是公共类型。

- 具有不带参数的公共构造函数。

- 不执行需要其他安全权限的代码。

- 仅公开读取/写入公共属性， (将忽略其他属性) 。

- )  (接受嵌套数组，而不公开多维数组。

- 不从属性和字段返回接口。

- <xref:System.Collections.IDictionary>如果集合，则不实现。

  缓存数据对象时， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 会将对象序列化为一个 XML 字符串，该字符串存储在文档的 *自定义 XML 部件* 中。 有关详细信息，请参阅 [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

## <a name="cached-data-size-limits"></a>缓存数据大小限制
 对于可以添加到文档中的数据缓存的数据总量以及数据缓存中任何单个对象的大小，有一些限制。 如果超过这些限制，则在将数据保存到数据缓存时，应用程序可能会意外关闭。

 若要避免这些限制，请遵循以下准则：

- 不要将大于 10 MB 的任何对象添加到数据缓存中。

- 不要将超过 100 MB 的总数据添加到单个文档中的数据缓存中。

  这些是大致值。 确切的限制取决于多个因素，包括可用 RAM 和正在运行的进程数。

## <a name="control-the-behavior-of-cached-objects"></a>控制缓存对象的行为
 若要更好地控制缓存对象的行为，可以 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 在缓存的对象的类型上实现接口。 例如，如果要控制在对象发生更改时通知用户的方式，则可以实现此接口。 有关演示如何实现的代码示例 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> ，请参阅 `ControlCollection` [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel 动态控件示例和 Word 动态控件示例中的类。

## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>保存对受密码保护的文档中的缓存数据所做的更改
 如果在受密码保护的文档中缓存数据对象，则不会保存对缓存数据所做的更改。 可以通过重写两个方法来保存对缓存数据所做的更改。 重写这些方法，以便在保存文档时暂时删除保护，然后在保存操作完成后重新应用保护。

 有关详细信息，请参阅 [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>在将 null 值添加到数据缓存时防止数据丢失
 将对象添加到数据缓存后，在保存和关闭文档之前，所有缓存的对象都必须初始化为非**null** 值。 如果在保存和关闭文档时，任何缓存对象的值都为 **null** ，则 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将自动从数据缓存中删除所有已缓存的对象。

 如果在设计时使用特性将具有 **null** 值的对象添加到数据缓存 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 中，则可以使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类在打开文档之前初始化缓存的数据对象。 如果要在最终用户打开文档之前，在未安装 Word 或 Excel 的服务器上初始化缓存的数据，则这非常有用。 有关详细信息，请参阅在 [服务器上访问文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="see-also"></a>另请参阅
- [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式在 Office 文档中缓存数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [演练：使用缓存的数据集创建主/从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)
