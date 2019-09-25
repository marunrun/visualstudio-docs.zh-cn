---
title: 访问服务器上文档中的数据
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
ms.openlocfilehash: ab033120c0913bbae33458c5a2d0b53972364581
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255769"
---
# <a name="access-data-in-documents-on-the-server"></a>访问服务器上文档中的数据
  您可以对文档级自定义项中的数据进行编程，而不必使用 Microsoft Office Word 或 Microsoft Office Excel 的对象模型。 这意味着，你可以访问服务器上的文档中包含的数据，该服务器未安装 Word 或 Excel。 例如，服务器上的代码（例如，在[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]页中）可以自定义文档中的数据，并将自定义文档发送给最终用户。 当最终用户打开文档时，解决方案程序集中的数据绑定代码会将自定义数据绑定到文档中。 这是可能的，因为文档中的数据与用户界面分开。 有关详细信息，请参阅[文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="cache-data-for-use-on-a-server"></a>缓存要在服务器上使用的数据
 若要在文档中缓存数据对象，请在设计时<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>用特性标记它，或在运行`StartCaching`时使用宿主项的方法。 当你在文档中缓存数据对象时，会[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]将对象序列化为存储在文档中的 XML 字符串。 对象必须满足某些要求才能进行缓存。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

 服务器端代码可以操作数据缓存中的任何数据对象。 绑定到缓存数据实例的控件与用户界面同步，因此在客户端上打开该文档时，对数据所做的任何服务器端更改都将自动显示。

## <a name="access-data-in-the-cache"></a>访问缓存中的数据
 可以从办公室以外的应用程序（例如，从控制台应用程序、Windows 窗体应用程序或网页）访问缓存中的数据。 访问缓存数据的应用程序必须具有完全信任;具有部分信任的 Web 应用程序无法插入、检索或更改在 Office 文档中缓存的数据。

 数据缓存可通过<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类的属性公开的集合的层次结构进行访问：

- 属性返回一个<xref:Microsoft.VisualStudio.Tools.Applications.CachedData>，它包含文档级自定义项中的所有缓存数据。 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>

- 每<xref:Microsoft.VisualStudio.Tools.Applications.CachedData>个都包含一个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>或多个对象。 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>包含在一个类中定义的所有缓存数据对象。

- 每<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>个都包含一个<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>或多个对象。 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>表示单个缓存的数据对象。

  下面的代码示例演示如何访问 Excel 工作簿项目的`Sheet1`类中的缓存字符串。 此示例摘自为<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A>方法提供的更大示例的一部分。

  [!code-csharp[Trin_ServerDocument#12](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#12)]
  [!code-vb[Trin_ServerDocument#12](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#12)]

## <a name="modify-data-in-the-cache"></a>修改缓存中的数据
 若要修改缓存的数据对象，通常需要执行以下步骤：

1. 将缓存的对象的 XML 表示形式反序列化为对象的新实例。 可以通过使用<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A>表示缓存数据对象的的属性<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem>来访问 XML。

2. 对此副本进行更改。

3. 使用以下选项之一将已更改的对象序列化回数据缓存：

    - 如果要自动序列化这些更改，请使用<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A>方法。 此方法使用**DiffGram**格式对数据缓存<xref:System.Data.DataSet>中的数据集对象进行序列化<xref:System.Data.DataTable>。 **DiffGram**格式确保将脱机文档中的数据缓存更改正确地发送到服务器。

    - 如果要对缓存数据的更改执行自己的序列化，则可以直接写入到<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A>属性。 如果使用 <xref:System.Data.Common.DataAdapter>对<xref:System.Data.DataSet>、或类型化数据集中的数据所做的更改更新数据库， <xref:System.Data.DataTable>请指定 DiffGram 格式。 否则， <xref:System.Data.Common.DataAdapter>将通过添加新行而不是修改现有行来更新数据库。

### <a name="modify-data-without-deserializing-the-current-value"></a>修改数据而不反序列化当前值
 在某些情况下，你可能想要修改缓存对象的值，而无需首先对当前值进行反序列化。 例如，如果要更改具有简单类型的对象（如字符串或整数）的值，或者如果要在服务器上的文档中初始化缓存<xref:System.Data.DataSet> ，则可以执行此操作。 在这些情况下，可以使用<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A>方法，无需先反序列化缓存对象的当前值。

 下面的代码示例演示如何在 Excel 工作簿项目的`Sheet1`类中更改缓存字符串的值。 此示例摘自为<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A>方法提供的更大示例的一部分。

 [!code-csharp[Trin_ServerDocument#11](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#11)]
 [!code-vb[Trin_ServerDocument#11](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#11)]

### <a name="modify-null-values-in-the-data-cache"></a>修改数据缓存中的 null 值
 保存并关闭文档时，数据缓存不会存储值**为 null**的对象。 修改缓存的数据时，此限制具有几个后果：

- 如果将数据缓存中的任何对象设置为**null**值，则在文档打开时，数据缓存中的所有对象都将自动设置为**null** ，并且在保存并关闭文档后，将清除整个数据缓存。 也就是说，所有缓存的对象都将从数据缓存中删除，并且<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>集合将为空。

- 如果您在数据缓存中生成一个包含**null**对象的解决方案，并且您希望在第一次打开<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>文档之前通过使用类来初始化这些对象，则必须确保您初始化数据缓存中的所有对象。 如果只初始化某些对象，则在文档打开时，所有对象都将设置为**null** ，并且在保存和关闭文档后将清除整个数据缓存。

## <a name="access-typed-datasets-in-the-cache"></a>访问缓存中的类型化数据集
 如果要从 office 解决方案和 office 外部的应用程序（例如 Windows 窗体应用程序或[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]项目）访问类型化数据集中的数据，则必须在两个中引用的单独程序集中定义类型化数据集投射. 如果使用 "**数据源配置**向导" 或 "**数据集设计器**向每个项目添加类型化数据集，则 .NET Framework 会将两个项目中的类型化数据集视为不同的类型。 有关创建类型化数据集的详细信息，请参阅[在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)