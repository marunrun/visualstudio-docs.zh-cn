---
title: 访问服务器上的文档中的数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d12c8168ef01dd3a38616af4f9dab2c38662bfff
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563100"
---
# <a name="access-data-in-documents-on-the-server"></a>访问服务器上的文档中的数据
  可以对其进行编程的文档级自定义项中的数据而无需使用的 Microsoft Office Word 或 Microsoft Office Excel 对象模型。 这意味着你可以访问的服务器上的不具有 Word 文档中包含的数据或安装 Excel。 例如，在服务器上的代码 (例如，在[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]页) 可以自定义文档中的数据和自定义的文档发送给最终用户。 当最终用户打开文档时，解决方案程序集中的数据绑定代码将自定义的数据绑定到文档中。 这可能是因为在文档中的数据分隔从用户界面。 有关详细信息，请参阅[缓存的文档级自定义项中的数据](../vsto/cached-data-in-document-level-customizations.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="cache-data-for-use-on-a-server"></a>在服务器上使用的缓存数据
 若要缓存在文档中的数据对象，将其与标记<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>在设计时属性，或使用`StartCaching`在运行时主机项的方法。 当缓存数据对象在文档中，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]对象序列化为 XML 字符串存储在文档中。 对象必须满足某些要求，才可进行缓存。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

 服务器端代码可以操作的数据缓存中的任何数据对象。 控件绑定到缓存的数据实例，以便对数据所做的任何服务器端更改会自动显示在客户端上打开文档时与用户界面中，同步。

## <a name="access-data-in-the-cache"></a>访问缓存中的数据
 您可以从外部 Office，例如从一个控制台应用程序、 Windows 窗体应用程序或网页的应用程序访问缓存中的数据。 访问缓存的数据的应用程序必须具有完全信任;具有部分信任的 Web 应用程序不能插入、 检索或更改在 Office 文档中缓存的数据。

 数据缓存是可通过公开的集合的层次结构访问<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>属性的<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类：

- <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>属性返回<xref:Microsoft.VisualStudio.Tools.Applications.CachedData>，它包含所有的文档级自定义项中缓存的数据。

- 每个<xref:Microsoft.VisualStudio.Tools.Applications.CachedData>包含一个或多个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>对象。 一个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>包含所有单个类中定义的缓存的数据对象。

- 每个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>包含一个或多个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>对象。 一个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>表示单个缓存的数据对象。

  下面的代码示例演示如何访问中的缓存的字符串`Sheet1`的 Excel 工作簿项目的类。 此示例是为提供一个更大示例的一部分<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A>方法。

  [!code-csharp[Trin_ServerDocument#12](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#12)]
  [!code-vb[Trin_ServerDocument#12](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#12)]

## <a name="modify-data-in-the-cache"></a>修改缓存中的数据
 若要修改的缓存的数据对象，通常执行以下步骤：

1. 反序列化的 XML 表示形式的缓存对象到对象的新实例。 可以使用访问 XML<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A>属性的<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>，表示缓存的数据对象。

2. 请对此副本所做的更改。

3. 序列化为已更改的对象返回的数据缓存通过使用以下选项之一：

    - 如果你想要自动序列化所做的更改，使用<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A>方法。 此方法使用**DiffGram**格式进行序列化<xref:System.Data.DataSet>， <xref:System.Data.DataTable>，和类型的数据缓存中的数据集对象。 **DiffGram**格式可确保更改脱机文档中的数据缓存正确发送到服务器。

    - 如果你想要对缓存数据的更改执行你自己的序列化，您可以直接写<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A>属性。 指定**DiffGram**如果你使用格式化<xref:System.Data.Common.DataAdapter>中的数据所做的更改更新数据库<xref:System.Data.DataSet>， <xref:System.Data.DataTable>，或类型化数据集。 否则为<xref:System.Data.Common.DataAdapter>将通过添加新行，而不是修改现有的行更新数据库。

### <a name="modify-data-without-deserializing-the-current-value"></a>修改数据，而不反序列化的当前值
 在某些情况下，你可能想要修改的缓存的对象值，而第一个的反序列化的当前值。 例如，你可以执行此操作或如果要更改的值的对象具有简单类型，如字符串或整数，如果正在初始化缓存<xref:System.Data.DataSet>在服务器上的文档。 在这些情况下，你可以使用<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A>方法，而第一个的反序列化的缓存对象的当前值。

 下面的代码示例演示如何更改缓存中的字符串值`Sheet1`的 Excel 工作簿项目的类。 此示例是为提供一个更大示例的一部分<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A>方法。

 [!code-csharp[Trin_ServerDocument#11](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#11)]
 [!code-vb[Trin_ServerDocument#11](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#11)]

### <a name="modify-null-values-in-the-data-cache"></a>修改数据缓存中的 null 值
 数据缓存不会存储具有的值的对象**null**保存和关闭文档时。 当修改缓存的数据时，此限制具有以下若干影响：

- 如果设置的任何对象中的值的数据缓存**null**，所有数据缓存中的对象将自动设置为**null**时将打开文档，并且整个数据缓存将被清除时保存和关闭文档。 所有缓存对象，即删除从数据缓存和<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>集合将为空。

- 如果生成使用的解决方案**null**中的对象的数据缓存和你想要使用初始化这些对象<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类文档前的首次打开时，您必须确保您初始化的所有对象中的数据缓存。 如果只有某些对象初始化的所有对象将设置为**null**时打开文档，并保存并关闭文档时，将清除整个数据缓存。

## <a name="access-typed-datasets-in-the-cache"></a>在缓存中的访问类型化数据集
 如果你想要从 Office 解决方案和外部的应用程序 Office，例如 Windows 窗体应用程序中访问中的类型化数据集的数据或[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]项目中，您必须在单独的程序集引用中定义类型化数据集项目。 将类型化数据集到每个项目添加通过使用**数据源配置**向导或**数据集设计器**，.NET Framework 将处理为不同类型的两个项目的类型化数据集. 有关创建类型化数据集的详细信息，请参阅[创建和配置 Visual Studio 中的数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [文档级自定义项中的缓存的数据](../vsto/cached-data-in-document-level-customizations.md)