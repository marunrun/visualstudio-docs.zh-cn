---
title: 按 Office 应用程序和项目类型提供的功能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio]
- Office development in Visual Studio, features
- Ribbon [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], features available
- document-level customizations [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], features available
- add-ins [Office development in Visual Studio]
- form regions [Office development in Visual Studio], features available
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: df645fc7f53bbcd0ad5294182d13e96b57b5d42d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431578"
---
# <a name="features-available-by-office-application-and-project-type"></a>按 Office 应用程序和项目类型提供的功能
  Visual Studio 具有几种类型的项目模板，它们支持 Microsoft Office 应用程序的不同业务方案，包括以下类型：

- 文档级自定义项。

- VSTO 外接程序

  并非所有应用程序都可以使用所有项目类型。 例如，文档级项目仅可用于 Microsoft Office Word 和 Microsoft Office Excel。 同样，某些功能仅可用于特定类型的项目或应用程序。 例如，操作窗格仅在文档级项目中可用，而功能区扩展仅可用于某些应用程序。 有关不同的项目类型的详细信息，请参阅[Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

> [!NOTE]
> Office 项目模板仅在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的某些版本中可用。 有关详细信息，请参阅[配置计算机以开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

## <a name="project-types-available-for-different-microsoft-office-applications"></a>可用的不同 Microsoft Office 应用程序的项目类型
 下表显示了可使用所有项目类型的应用程序。

|项目类型|Microsoft Office 应用程序|
|-------------------|----------------------------------|
|文档级自定义项|Excel<br /><br /> 字|
|VSTO 外接程序|Excel<br /><br /> InfoPath（仅 InfoPath 2013 和 InfoPath 2010）<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> 项目<br /><br /> Visio<br /><br /> 字<br /><br /> Excel|

## <a name="features-available-in-different-project-types"></a>在不同的项目类型中可用的功能
 下表显示了提供每项功能的项目类型。

|功能|提供该功能的项目类型|其他阅读材料|
|-------------|--------------------------------------------|---------------------|
|操作窗格。|文档级项目。|[操作窗格概述](../vsto/actions-pane-overview.md)|
|ClickOnce 部署。|VS 与文档级项目。|[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)|
|自定义任务窗格。|以下应用程序的 VSTO 外接程序项目：<br /><br /> -   Excel<br />-InfoPath （InfoPath 2013 和 InfoPath 2010 仅）<br />-   Outlook<br />-   PowerPoint<br />-   Word|[自定义任务窗格](../vsto/custom-task-panes.md)|
|自定义 XML 部件。|文档级项目。<br /><br /> 以下应用程序的应用程序级项目：<br /><br /> -   Excel<br />-   PowerPoint<br />-   Word|[自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)|
|数据缓存。|文档级项目。|[文档级自定义项中的缓存的数据](../vsto/cached-data-in-document-level-customizations.md)|
|公开 VSTO 外接程序中向其他 Microsoft Office 解决方案的对象。|VSTO 外接程序项目。|[从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)|
|以下主机控件：<br /><br /> -图表<br />-   ListObject<br />-   NamedRange<br />的内容控件<br />书签|文档级项目。<br /><br /> 用于 Word 和 Excel 的 VSTO 外接程序项目。|[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)|
|以下主机控件：<br /><br /> -   XMLMappedRange<br />-   XMLNode<br />-   XMLNodes|文档级项目。|[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)|
|多项目部署。|文档级项目。<br /><br /> VSTO 外接程序项目。|[演练：部署在单个 ClickOnce 安装程序中的多个 Office 解决方案](https://msdn.microsoft.com/051223c0-4082-4799-b78b-a4763a9def55)|
|Outlook 窗体区域。|用于 Outlook 的 VSTO 外接程序项目。|[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)|
|部署后操作。|文档级项目。<br /><br /> VSTO 外接程序项目。|[演练：在安装 ClickOnce 后将文档复制到最终用户计算机](https://msdn.microsoft.com/100090f7-bc63-4152-b3e1-19b48bc27466)|
|功能区自定义。|文档级项目。<br /><br /> 以下应用程序的 VSTO 外接程序项目：<br /><br /> -   Excel<br />-InfoPath （InfoPath 2013 和 InfoPath 2010 仅）<br />-   Outlook<br />-   PowerPoint<br />-   Project<br />-   Visio<br />-   Word|[功能区概述](../vsto/ribbon-overview.md)|
|可视化文档设计器。|文档级项目。|[在 Visual Studio 环境中的 office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)|

## <a name="see-also"></a>请参阅
- [开始&#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [文档级自定义项中的缓存的数据](../vsto/cached-data-in-document-level-customizations.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
