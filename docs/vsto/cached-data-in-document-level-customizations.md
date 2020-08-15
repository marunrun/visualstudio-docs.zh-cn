---
title: 文档级自定义项中的缓存数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data islands [Office development in Visual Studio]
- view [Office development in Visual Studio]
- caching data [Office development in Visual Studio], about caching data
- data caching [Office development in Visual Studio], about data caching
- data [Office development in Visual Studio], cache
- data [Office development in Visual Studio], document-level solutions
- document-level customizations [Office development in Visual Studio], data model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9985dd25ba62cc9c0735a8a8f4008a4c0abe0558
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238343"
---
# <a name="cached-data-in-document-level-customizations"></a>文档级自定义项中的缓存数据
  文档级自定义项的主要目标是在 Office 文档中将数据从视图中分离出来。 数据是指存储在文档中的信息，包括数字和文本。 视图引用 Microsoft Office Word 和 Microsoft Office Excel 的用户界面和对象模型。

 Visual Studio 通过允许将数据作为 *数据岛*嵌入（也称为 *数据缓存*），将数据从视图中的数据分离出来。 无需启动 Word 或 Excel 即可直接读取或修改数据。 当你需要修改未安装 Microsoft Office 的服务器上的文档中的数据时，这很有用。 Word 和 Excel 应在客户端环境中使用;它们不会在服务器上运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有关文档级自定义项的详细信息，请参阅 [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md) 和 [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="understand-the-cached-data-programming-model"></a>了解缓存的数据编程模型
 数据岛可以包含解决方案中满足特定要求的任何对象。 这些对象包括 <xref:System.Data.DataSet> 对象、 <xref:System.Data.DataTable> 对象以及可以由类序列化的任何其他对象 <xref:System.Xml.Serialization.XmlSerializer> 。 有关详细信息，请参阅 [缓存数据](../vsto/caching-data.md)。

 若要提供缓存数据的视图，您可以将文档上 Windows 窗体控件和 *宿主控件* 绑定到数据岛中的对象。 数据岛和数据绑定控件之间的数据绑定会使二者保持同步。 您还可以将验证代码添加到独立于控件的数据中。 有关详细信息，请参阅 [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

 宿主控件是 Excel 和 Word 对象模型中的本机对象的扩展版本。 与本机对象不同，主机控件可以直接绑定到托管数据对象。 有关详细信息，请参阅 [宿主项和宿主控件概述](../vsto/host-items-and-host-controls-overview.md) 和 [在 Office 文档上 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

## <a name="access-cached-data-on-the-server"></a>访问服务器上的缓存数据
 若要访问文档中的缓存数据，可以使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类。 此类是的一部分 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ，它可以在服务器上使用，而无需运行 Excel 或 Word。 当用户在修改缓存数据后打开文档时，绑定到数据的任何控件将自动同步到更改，并向用户显示更新的数据。 有关详细信息，请参阅在 [服务器上访问文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 不需要 Excel 和 Word 写入服务器上的数据，只需在客户端查看它。 甚至无需在服务器上安装 Excel 和 Word。 这可提高可伸缩性，并能够对包含数据岛的文档执行快速批处理。

## <a name="data-caching-for-offline-use"></a>用于脱机使用的数据缓存
 将数据存储在数据岛中可以实现脱机方案。 当用户首次打开文档或从服务器请求文档时，数据岛使用最新的数据进行填充。 数据岛缓存在文档中，然后可脱机使用。 即使没有可用的实时连接，用户 (和代码) 也可以操作数据。 用户重新连接时，对数据所做的更改可以传播回服务器数据源。

## <a name="cached-data-and-custom-xml-parts-compared"></a>比较缓存的数据和自定义 XML 部件
 在 2007 Microsoft Office 系统中引入了自定义 XML 部件，作为一种将任意部分 XML 存储在文档中的方法。 尽管自定义 XML 部件在许多与数据缓存相同的情况下很有用，但数据岛和自定义 XML 部件之间存在一些差异。 有关自定义 XML 部件的详细信息，请参阅 [自定义 xml 部件概述](../vsto/custom-xml-parts-overview.md)。

 下表列出了一些差异和相似性。

|问题/特征|数据缓存|自定义 XML 部件|
|-|----------------|----------------------|
|哪些 Office 应用程序可以使用这些应用程序？|以下应用程序的文档级自定义项：<br /><br /> -Excel<br />-Word|适用于以下应用程序的文档级和应用程序级解决方案：<br /><br /> -Excel<br />-PowerPoint<br />-Word|
|可以存储哪些类型的数据？|自定义程序集中满足特定要求的任何公共对象。 有关详细信息，请参阅 [缓存数据](../vsto/caching-data.md)。|任何 XML 数据。|
|能否在不启动 Microsoft Office 应用程序的情况下访问数据？|是，通过使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 提供的类 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。|是，通过使用命名空间中的类 <xref:System.IO.Packaging> ，或使用 OPEN XML 格式 SDK。|

## <a name="see-also"></a>另请参阅
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [Visual Studio 中 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
