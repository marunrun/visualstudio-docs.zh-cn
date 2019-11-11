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
ms.openlocfilehash: b064df6729b914af7758cde86b03b886fd0e5d26
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72986264"
---
# <a name="form-support-in-workflows"></a>工作流中的窗体支持
  可以在工作流中使用四种类型的窗体：关联、启动、任务和修改。 这些窗体类型可以基于 ASPX 窗体或 InfoPath 窗体。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 为特定窗体提供的支持级别取决于若干因素，如下表中所述。 有关工作流窗体类型的详细信息，请参阅[工作流窗体概述](/previous-versions/office/developer/sharepoint-2010/ms457061(v=office.14))。

## <a name="xml-refactoring"></a>XML 重构
 将 ASPX 关联或启动窗体添加到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流项目项时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会自动重构工作流的*元素 .xml*文件中的 xml，以使引用关联或启动窗体的属性保持同步每当更新窗体名称或部署路径或删除窗体时。 但是，在工作流中使用其他窗体类型（如任务或修改窗体）时，不会重构*元素 .xml*文件。

## <a name="form-support-in-new-visual-studio-workflows"></a>新 Visual Studio 工作流中的窗体支持
 下表列出了在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建的工作流的 ASPX 或 InfoPath 窗体上的不同窗体类型 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持。

|表单类型|在 Visual Studio 中使用 ASPX 形式创建的工作流|使用 InfoPath 表单在 Visual Studio 中创建的工作流|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|关联|-通过使用**工作流关联窗体**项模板，可以将 ASPX 关联窗体添加到工作流中。<br />-当添加、重命名或删除窗体时，或者当窗体的部署路径更改时，将重构工作流的*元素 .xml*文件。<br />-有关详细信息，请参阅[演练：使用关联窗体和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 InfoPath 关联窗体模板。<br />-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-不重构工作流的*元素 .xml*文件。|
|初始|-可以使用**工作流启动窗体**项模板将 ASPX 启动窗体添加到工作流。<br />-当添加、重命名或删除窗体时，或者当窗体的部署路径更改时，将重构工作流的*元素 .xml*文件。<br />-有关详细信息，请参阅[演练：使用关联窗体和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 InfoPath 关联窗体模板。<br />-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-不重构工作流的*元素 .xml*文件。|
|任务|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 ASPX 任务窗体模板。 您必须创建一个应用程序页并向其中添加代码。<br />-不重构工作流的*元素 .xml*文件。<br />-有关详细信息，请参阅[工作流任务窗体（SharePoint Foundation）](/previous-versions/office/developer/sharepoint-2010/ms438856(v=office.14))|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 InfoPath 任务窗体模板。<br />-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-不重构工作流的*元素 .xml*文件。|
|做|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 ASPX 修改窗体模板。 若要添加修改窗体，必须创建应用程序页并向其添加代码。<br />-不重构工作流的*元素 .xml*文件。 您必须根据需要手动对其进行编辑。<br />-有关详细信息，请参阅[工作流修改窗体（SharePoint Foundation）](/previous-versions/office/developer/sharepoint-2010/ms480794(v=office.14))|-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中没有 InfoPath 修改窗体模板。<br />-[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-不重构工作流的*元素 .xml*文件。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>导入 SharePoint 可重用工作流中的窗体支持
 下表列出了对导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]的 SharePoint 可重用工作流中的 ASPX 或 InfoPath 表单上的不同窗体类型 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持。

|表单类型|从 SharePoint Designer 导入了 ASPX 表单的可重用工作流|从 SharePoint Designer 导入 InfoPath 窗体的可重用工作流|
|---------------|-------------------------------------------------------------------------------| - |
|关联|-在工作流的*元素 .xml*文件中引用此窗体。<br />-重命名或删除窗体或其部署路径更改时，将重构工作流的*元素 .xml*文件。|-导入了窗体，但在工作流的*xml*中未引用此窗体。<br />-不重构工作流的*元素 .xml*文件。|
|初始|-工作流在工作流的*元素 .xml*文件中引用了该窗体。<br />-重命名或删除窗体或其部署路径更改时，将重构工作流的*元素 .xml*文件。|-导入了窗体，但在工作流的*xml*中未引用此窗体。<br />-不重构工作流的*元素 .xml*文件。 **注意：** 若要运行此方案，必须添加和更改规则和属性。|
|任务|-在工作流的*元素 .xml*文件中引用此窗体。<br />-不重构工作流的*元素 .xml*文件。|-导入了窗体，但在工作流的*xml*中未引用此窗体。<br />-不重构工作流的*元素 .xml*文件。 **注意：** 若要运行此方案，必须添加和更改规则和属性。|
|做|不适用。 无法在 SharePoint 设计器中创建 ASPX 修改窗体。|不适用。 InfoPath 修改窗体不能在 SharePoint 设计器中创建，内置 SharePoint Server 工作流除外，导出工作流时，该工作流不会包含在 .wsp 文件中。|

## <a name="see-also"></a>请参阅
- [演练：创建具有关联窗体和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [从现有 SharePoint 站点导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
