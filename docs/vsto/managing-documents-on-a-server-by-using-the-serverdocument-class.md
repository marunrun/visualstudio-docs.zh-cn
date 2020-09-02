---
title: 使用 ServerDocument 类管理服务器上的文档
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], managing on server
- Office documents [Office development in Visual Studio, managing on server
- ServerDocument class, managing documents on server
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 739946fc7fc6ea7014fb93010ca85094a7fc7056
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "71251937"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>使用 ServerDocument 类管理服务器上的文档
  你可以使用 `ServerDocument` 中的类 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 来管理文档级自定义项的多个方面，即使未安装 Microsoft Office Word 和 Microsoft Office Excel。 你可以执行下列任务：

- 访问和修改文档或工作簿的数据缓存中的数据。 有关详细信息，请参阅 [在文档中使用缓存数据](#CachedData)。

- 管理与文档相关联的自定义项程序集。 有关详细信息，请参阅 [管理文档自定义](#CustomizationInfo)。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="understand-the-serverdocument-class"></a>了解 ServerDocument 类
 `ServerDocument`类设计为在未安装 Office 的计算机上使用。 因此，通常在不与 Office 集成的应用程序（例如，控制台项目或 Windows 窗体项目，而不是 Office 项目）中使用此类。 使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* 程序集中的类。

 `ServerDocument`类可用于在使用创建的文档级自定义项上操作 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 。

 有关 Visual Studio 2010 Tools for Office Runtime 和 .NET Framework 的 Office 扩展的详细信息，请参阅 [Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

> [!NOTE]
> 如果有使用 `ServerDocument` `Visual Studio Tools for Office` system (版本3.0 运行时) 中的类的旧版应用程序，则 `Visual Studio Tools for Office` 必须在运行该应用程序的计算机上安装系统 (版本3.0 运行时) 。 `Visual Studio 2010 Tools for Office runtime`无法运行这些应用程序。

## <a name="work-with-cached-data-in-the-document"></a><a name="CachedData"></a> 处理文档中的缓存数据
 `ServerDocument`类提供可用于在自定义文档中处理数据缓存的成员。 有关缓存数据的详细信息，请参阅在服务器上 [缓存数据](../vsto/caching-data.md) 和 [访问文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 下表列出了可用于处理缓存数据的成员。

|任务|供使用的成员|
|----------|-------------------|
|确定文档是否有数据缓存。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A> 方法。|
|访问文档中的缓存数据。<br /><br /> 有关详细信息，请参阅在 [服务器上访问文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 属性。|

## <a name="manage-the-document-customization"></a><a name="CustomizationInfo"></a> 管理文档自定义
 您可以使用类的成员 `ServerDocument` 来管理与文档相关联的自定义项程序集。 例如，你可以以编程方式从文档中删除自定义项，以使该文档不再是自定义项的一部分。

 下表列出了可用于管理自定义项程序集的成员。

|任务|供使用的成员|
|----------|-------------------|
|确定文档是否为文档级自定义项的一部分。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A> 方法。|
|在运行时以编程方式将自定义项附加到文档。<br /><br /> 有关详细信息，请参阅 [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)|其中一种 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> 方法。|
|在运行时以编程方式从文档中删除自定义项。<br /><br /> 有关详细信息，请参阅 [如何：从文档中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> 方法。|
|获取与文档关联的部署清单的 URL。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> 属性。|

## <a name="see-also"></a>另请参阅
- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
- [如何：从文档中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [缓存数据](../vsto/caching-data.md)
