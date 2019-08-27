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
ms.openlocfilehash: 82763f78673391ab6a308ba026a6b9e53c3b474b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438826"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>使用 ServerDocument 类管理服务器上的文档
  可以使用`ServerDocument`类中[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]来管理文档级自定义的几个方面，即使未安装 Microsoft Office Word 和 Microsoft Office Excel。 您可以执行以下任务：

- 访问和修改文档或工作簿的数据缓存中的数据。 有关详细信息，请参阅[处理的文档中的缓存数据](#CachedData)。

- 管理与文档相关联的自定义程序集。 有关详细信息，请参阅[管理文档自定义项](#CustomizationInfo)。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="understand-the-serverdocument-class"></a>了解 ServerDocument 类
 `ServerDocument`类旨在在没有安装 Office 的计算机上使用。 因此，您通常使用此类应用程序不与集成 Office，如控制台项目或 Windows 窗体项目，而不是 Office 项目中。 使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类中*Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll*程序集。

 `ServerDocument`类可用于对文档级自定义项创建的使用[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]。

 详细了解 Visual Studio 2010 Tools for Office Runtime 和 Office 扩展的.NET Framework，请参阅[Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

> [!NOTE]
> 如果已使用的旧应用程序`ServerDocument`类中`Visual Studio Tools for Office`系统 (版本 3.0 运行时)，则`Visual Studio Tools for Office`必须运行该应用程序的计算机上安装系统 （版本 3.0 运行时）。 `Visual Studio 2010 Tools for Office runtime`无法运行这些应用程序。

## <a name="CachedData"></a> 使用文档中的缓存数据
 `ServerDocument`类提供了可用于使用自定义文档中的数据缓存的成员。 有关缓存数据的详细信息，请参阅[缓存数据](../vsto/caching-data.md)并[访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 下表列出了可用于使用缓存数据的成员。

|任务|供使用的成员|
|----------|-------------------|
|若要确定文档是否具有数据缓存。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A> 方法。|
|若要访问在文档中缓存的数据。<br /><br /> 有关详细信息，请参阅[访问服务器上的文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 属性。|

## <a name="CustomizationInfo"></a> 管理文档自定义项
 可以使用的成员`ServerDocument`类来管理与文档相关联的自定义程序集。 例如，你可以以编程方式自定义项从文档中删除，以便文档不再是一个自定义的一部分。

 下表列出了可用于管理自定义程序集的成员。

|任务|供使用的成员|
|----------|-------------------|
|若要确定文档是否是文档级自定义的一部分。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A> 方法。|
|若要以编程方式将自定义项附加在运行时向文档中。<br /><br /> 有关详细信息，请参阅[如何：将托管的代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)|其中一个<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A>方法。|
|若要在运行时以编程方式删除文档中的自定义项。<br /><br /> 有关详细信息，请参阅[如何：删除文档中的托管的代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> 方法。|
|若要获取与文档相关联的部署清单的 URL。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> 属性。|

## <a name="see-also"></a>请参阅
- [如何：将托管的代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
- [如何：删除文档中的托管的代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [缓存数据](../vsto/caching-data.md)
