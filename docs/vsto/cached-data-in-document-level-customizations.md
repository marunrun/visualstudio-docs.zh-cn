---
title: 文档级自定义项中的缓存的数据
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
ms.openlocfilehash: 62b0d04e37072af1f0053a6e395edcb856a115c1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939314"
---
# <a name="cached-data-in-document-level-customizations"></a>文档级自定义项中的缓存的数据
  文档级自定义项的主要目标是将数据从 Office 文档中的视图。 数据是指存储在文档中，包括数字和文本的信息。 视图是指用户界面和 Microsoft Office Word 和 Microsoft Office Excel 对象模型。

 Visual Studio 将数据从文档级自定义项中的视图分离通过使数据能够作为嵌入*数据岛*，也称为*数据缓存*。 可读取或修改的数据直接而无需启动 Word 或 Excel。 当您需要在没有安装 Microsoft Office 安装的服务器上的文档中修改数据时，这很有用。 Word 和 Excel 专门用于客户端环境;它们不被设计的服务器上运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有关文档级自定义项的详细信息，请参阅[Office 解决方案开发概述&#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md)并[体系结构的文档级自定义项](../vsto/architecture-of-document-level-customizations.md)。

## <a name="understand-the-cached-data-programming-model"></a>了解缓存的数据编程模型
 数据岛可以包含满足某些要求的解决方案中的任何对象。 这些对象包括<xref:System.Data.DataSet>对象，<xref:System.Data.DataTable>对象和任何其他对象，该对象可以序列化<xref:System.Xml.Serialization.XmlSerializer>类。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

 若要提供的缓存数据的视图，可以将绑定 Windows 窗体控件和*主机控件*数据岛中的对象在文档上。 数据岛和数据绑定控件之间的数据绑定使二者保持同步。 此外可以将验证代码添加到独立于控件的数据。 有关详细信息，请参阅[将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

 主机控件被扩展版本的 Excel 和 Word 对象模型中的本机对象。 与本机对象，不同宿主控件可以绑定直接到托管的数据对象。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)并[Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

## <a name="access-cached-data-on-the-server"></a>访问缓存服务器上的数据
 若要访问文档中的缓存的数据，可以使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类。 此类属于[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，可以在未正在运行的 Excel 或 Word 的服务器上使用它。 当用户打开文档时修改的缓存的数据，任何控件绑定到数据的自动同步到所做的更改，并且用户会看到更新后的数据。 有关详细信息，请参阅[访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 Excel 和 Word 不需要在服务器上，仅用于在客户端上查看它写入数据。 Excel 和 Word 不甚至需要在服务器上安装。 这提供了改进的可伸缩性和执行包含数据岛的文档的快速的批处理操作的能力。

## <a name="data-caching-for-offline-use"></a>数据缓存以供脱机使用
 将数据存储在数据岛中支持脱机方案。 当用户首次打开文档或从服务器请求文档时，使用最新的数据填充数据岛。 数据岛缓存到文档中，然后可脱机。 用户 （和你的代码） 可以处理的数据中，即使没有实时连接可用。 当用户重新连接时，对数据的更改可以传播回数据源。

## <a name="cached-data-and-custom-xml-parts-compared"></a>缓存的数据和比较的自定义 XML 部件
 作为一种方法来存储在文档中的任意 XML 片段中 2007 Microsoft Office 系统引入了自定义 XML 部件。 尽管自定义 XML 部件中的许多数据缓存为相同的方案非常有用，但有的数据岛和自定义 XML 部件之间的一些差异。 有关自定义 XML 部件的详细信息，请参阅[自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

 下表列出了一些差异和相似之处。

||数据缓存|自定义 XML 部件|
|-|----------------|----------------------|
|哪些 Office 应用程序可以使用这些？|以下应用程序的文档级自定义：<br /><br /> -   Excel<br />-   Word|以下应用程序的文档级和应用程序级别解决方案：<br /><br /> -   Excel<br />-   PowerPoint<br />-   Word|
|您可以存储哪些类型的数据？|中满足某些要求将自定义程序集的任何公共对象。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。|任何 XML 数据。|
|您可以访问而无需启动 Microsoft Office 应用程序的数据？|是的通过使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类提供的[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。|是的通过使用中的类<xref:System.IO.Packaging>命名空间，或使用 Open XML 格式 SDK。|

## <a name="see-also"></a>请参阅
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [Visual Studio 中的 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
