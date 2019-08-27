---
title: 工作流中的窗体支持 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 704e08524bb9aaf014dbd29e7df7361a7e1bbefe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967404"
---
# <a name="form-support-in-workflows"></a>在工作流中的窗体支持
  可以在工作流中使用四种类型的窗体： 关联、 初始化、 任务和修改。 这些窗体类型可以基于 ASPX 窗体或 InfoPath 窗体。 级别支持[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]提供了用于特定窗体取决于若干因素下, 表中所述。 有关工作流窗体类型的详细信息，请参阅[工作流窗体概述](http://go.microsoft.com/fwlink/?LinkId=185228)。

## <a name="xml-refactoring"></a>XML 重构
 当您添加到 ASPX 关联或启动窗体[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]工作流项目项[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]自动重构工作流中的 XML *Elements.xml*要保留引用关联的属性文件或启动窗体保持同步每次更新窗体或部署路径时或在窗体已被删除。 但是，如果使用其他窗体类型在工作流，如任务或修改窗体中*Elements.xml*不重构文件。

## <a name="form-support-in-new-visual-studio-workflows"></a>在新的 Visual Studio 工作流中的窗体支持
 下表列出[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建的工作流中的 ASPX 或 InfoPath 窗体上的不同窗体类型的支持[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

|窗体类型|在 Visual Studio 中使用 ASPX 窗体中创建的工作流|在 Visual Studio 中创建使用 InfoPath 窗体的工作流|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|关联|-一个 ASPX 关联窗体可以通过使用添加到工作流**工作流关联窗体**项模板。<br />- *Elements.xml*添加、 重命名或删除在窗体时，或其部署路径更改时的要求进行重构的工作流的文件。<br />-有关详细信息，请参阅[演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-没有 InfoPath 关联窗体模板中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。<br />-没有之间集成[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和 InfoPath 设计器。<br />- *Elements.xml*不重构工作流的文件。|
|启动|-ASPX 初始化窗体可以通过使用添加到工作流**工作流发起窗体**项模板。<br />- *Elements.xml*添加、 重命名或删除在窗体时，或其部署路径更改时的要求进行重构的工作流的文件。<br />-有关详细信息，请参阅[演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-没有 InfoPath 关联窗体模板中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。<br />-没有之间集成[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和 InfoPath 设计器。<br />- *Elements.xml*不重构工作流的文件。|
|任务|-无 ASPX 任务窗体模板现已推出[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 必须创建应用程序页，并向其中添加代码。<br />- *Elements.xml*不重构工作流的文件。<br />-有关详细信息，请参阅[工作流任务窗体 (SharePoint Foundation)](http://go.microsoft.com/fwlink/?LinkId=187674)|-没有 InfoPath 任务窗体模板中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。<br />-没有之间集成[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和 InfoPath 设计器。<br />- *Elements.xml*不重构工作流的文件。|
|修改|-无 ASPX 修改窗体模板现已推出[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 若要添加修改窗体，必须创建应用程序页，并向其中添加代码。<br />- *Elements.xml*不重构工作流的文件。 您必须手动编辑它根据需要。<br />-有关详细信息，请参阅[工作流修改窗体 (SharePoint Foundation)](http://go.microsoft.com/fwlink/?LinkId=187675)|-没有 InfoPath 修改窗体模板中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。<br />-没有之间集成[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和 InfoPath 设计器。<br />- *Elements.xml*不重构工作流的文件。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>导入 SharePoint 可重用工作流中的窗体支持
 下表列出[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]支持将导入到的 SharePoint 可重用工作流中的 ASPX 或 InfoPath 窗体上的不同的窗体类型[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

|窗体类型|已从 SharePoint Designer 中导入的 ASPX 窗体的可重用工作流|已从 SharePoint Designer 中导入的 InfoPath 窗体的可重用工作流|
|---------------|-------------------------------------------------------------------------------| - |
|关联|的在中引用窗体*Elements.xml*工作流的文件。<br />- *Elements.xml*重命名或删除在窗体时，或其部署路径更改时的要求进行重构的工作流的文件。|的导入，但未在中引用窗体*Elements.xml*的工作流。<br />- *Elements.xml*不重构工作流的文件。|
|启动|的中的工作流引用窗体*Elements.xml*工作流的文件。<br />- *Elements.xml*重命名或删除在窗体时，或其部署路径更改时的要求进行重构的工作流的文件。|的导入，但未在中引用窗体*Elements.xml*的工作流。<br />- *Elements.xml*不重构工作流的文件。 **注意：** 规则和属性必须添加和更改此方案能够工作。|
|任务|的在中引用窗体*Elements.xml*工作流的文件。<br />- *Elements.xml*不重构工作流的文件。|的导入，但未在中引用窗体*Elements.xml*的工作流。<br />- *Elements.xml*不重构工作流的文件。 **注意：** 规则和属性必须添加和更改此方案能够工作。|
|修改|不适用。 不能在 SharePoint Designer 中创建修改的 ASPX 窗体。|不适用。 除了内置的 SharePoint Server 工作流，工作流导出时不包括.wsp 文件中，不能在 SharePoint Designer 中创建 InfoPath 修改窗体。|

## <a name="see-also"></a>请参阅
- [演练：使用关联和初始化表单创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [从现有的 SharePoint 网站导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
