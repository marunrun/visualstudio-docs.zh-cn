---
title: Microsoft Office 的不同版本中运行的解决方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], multiple Office versions
- Office applications [Office development in Visual Studio], multiple Office versions
- Office development in Visual Studio, multiple Office versions
- Office solutions [Office development in Visual Studio]
- multiple Office versions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4db3b9694ed8a21786933c3975e9f0970f60c7aa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978414"
---
# <a name="run-solutions-in-different-versions-of-microsoft-office"></a>Microsoft Office 的不同版本中运行的解决方案

## <a name="run-office-solutions-created-by-using-visual-studio-2010-and-above"></a>运行 Office 解决方案创建通过使用 Visual Studio 2010 及更高版本

|项目模板面向的 Office 版本|面向.NET Framework 的项目<sup>1</sup>|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|
|--------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|-------------------------------------------|
|Office 2016 和 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office 系统<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office 系统<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|.NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Visual Studio 2010 Tools for Office Runtime|
|2007 Microsoft Office system|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，<br /><br /> 或<br /><br /> .NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office Runtime|

 1. .NET Framework 版本上运行你的解决方案的最终用户计算机所需项目所面向的。 例如，如果项目面向.NET Framework 3.5，最终用户计算机上需要.NET Framework 3.5。 在此示例中，你的解决方案将不运行是否仅[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]最终用户计算机上安装。

 2. 在此情景中，只有当解决方案不使用 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 中的新功能时，它才会在 2007 Microsoft Office System 中正常运行。

## <a name="run-office-solutions-created-by-using-versions-of-visual-studio-prior-to-visual-studio-2010"></a>运行使用 Visual Studio 2010 之前的 Visual Studio 的版本创建的 Office 解决方案
 可以运行使用 Visual Studio 2010 之前的 Visual Studio 版本创建的解决方案的 Microsoft Office 应用程序。 在某些情况下，这些解决方案要求使用 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的不同版本。 不同版本的[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]可以在同一台计算机上并行安装。

 下表显示了哪些版本的 Microsoft Office 可以运行使用 Visual Studio 的早期版本创建的解决方案和哪些版本的[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]和.NET Framework 所需的每个解决方案。

|用于创建解决方案的 Visual Studio 版本|项目模板面向的 Office 版本|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|最终用户计算机上所需的.NET Framework 版本|
|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|-------------------------------------------|----------------------------------------------------------|
|Visual Studio 2008 专业版<br /><br /> 或<br /><br /> Visual Studio Team System 2008|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 并[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] <sup>1</sup><br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office Runtime<sup>1</sup><br /><br /> 或<br /><br /> Visual Studio Tools for the Microsoft Office System（3.0 版 Runtime）|.NET Framework 3.5|
|以下版本的 Visual Studio 2005 中使用 VSTO 2005 SE 之一<sup>2</sup>安装：<br /><br /> -Visual Studio 2005 Tools for Office<br />-   Visual Studio Team System 2005<br />-   Visual Studio 2005 Professional|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 并[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)](仅限 32 位<sup>3</sup>)<br /><br /> 2007 Microsoft Office system|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|
|Visual Studio 以下版本中的任何版本：<br /><br /> -   Visual Studio 2008 Professional<br />-Visual Studio Team System 2008<br />-Visual Studio 2005 Tools for Office (VSTO 2005 SE 无论<sup>2</sup>安装)<br />-Visual Studio Team System 2005 (带有或不带 VSTO 2005 SE<sup>2</sup>安装)<br />-使用 VSTO 2005 SE visual Studio 2005 Professional<sup>2</sup>安装|Microsoft Office 2003|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 并[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)](仅限 32 位<sup>3</sup>)<br /><br /> 2007 Microsoft Office system<br /><br /> Microsoft Office 2003|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|

 1. [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]应用程序包括 Visual Studio 2010 Tools for Office 运行时。 因此，这些应用程序始终使用 Visual Studio 2010 Tools for Office 运行时，而不是 Visual Studio 工具 Microsoft Office system (3.0 版运行时) 在此方案中。 2007 Microsoft Office System 中的应用程序可以使用 Visual Studio 2010 Tools Office 运行时或 Visual Studio Tools for Microsoft Office System（3.0 版 Runtime）。

 2. VSTO 2005 SE 是免费的 Visual Studio 外接程序，它提供 Microsoft Office 2003 和 2007 Microsoft Office 系统的 VSTO 外接程序项目模板。 可以通过 Visual Studio 2005 专业版、Visual Studio 2005 Tools for Office 或 Visual Studio Team System 2005 的某一版本安装它。 有关详细信息，请参阅[Visual Studio 2005 Tools for Office Second Edition](http://go.microsoft.com/fwlink/?LinkId=148446)。

 3. 需要 Visual Studio 2005 Tools for Office Second Edition Runtime 的 Office 解决方案与 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本不兼容。 若要在 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 或 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本中运行这些解决方案，必须将项目升级为 [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] 或面向 2007 Microsoft Office System 的 Visual Studio 2008 项目。

## <a name="see-also"></a>请参阅
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio Tools for Office runtime 安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [配置计算机以开发 Office 解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
