---
title: 托管参考 (Visual Studio 中的 Office 开发)
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reference [Office development in Visual Studio], 2007 Microsoft Office system
- Office development in Visual Studio, reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: da10833f8340d5308321038bb0500ca8408b40bb
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551764"
---
# <a name="managed-reference-office-development-in-visual-studio"></a>托管参考 (Visual Studio 中的 Office 开发)
  本部分包含在针对 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]的 Office 项目中使用的命名空间和类型的 API 参考文档。 有关面向 .NET Framework 3.5 的 Office 项目中使用的命名空间和类型的 API 参考文档, 请参阅 Visual Studio 文档中的以下参考部分: [http://go.microsoft.com/fwlink/?LinkId=160658](http://go.microsoft.com/fwlink/?LinkId=160658)。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>本节内容
 <xref:Microsoft.Office.Tools>

 包含对 Office 解决方案编程通用的类。 这些类包括 VSTO 加载项的基类、用于在 VSTO 加载项中创建自定义任务窗格的类、用于在 Excel 和 Word 解决方案中创建智能标记的类以及用于在文档级自定义项中创建操作窗格的类。

 <xref:Microsoft.Office.Tools.Excel>

 包含可以在 Excel 解决方案中使用的宿主控件和宿主项。

 <xref:Microsoft.Office.Tools.Excel.Controls>

 包含可以在 Excel 解决方案中使用的 Excel 控件和 Windows 窗体控件。

 <xref:Microsoft.Office.Tools.Outlook>

 包含 VSTO 加载项用于 Outlook 的类，包括用于创建自定义窗体区域的类。

 <xref:Microsoft.Office.Tools.Ribbon>

 包含用于以编程方式修改使用功能区设计器创建的功能区自定义项的类。

 <xref:Microsoft.Office.Tools.Word>

 包含可以在 Word 解决方案中使用的宿主控件和宿主项。

 <xref:Microsoft.Office.Tools.Word.Controls>

 包含可以在 Word 解决方案中使用的 Word 控件和 Windows 窗体控件。

 <xref:Microsoft.VisualStudio.Tools.Applications>

 包含 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类和一组相关的缓存数据类。 这些类可以用于在没有安装 Microsoft Office 的计算机上修改文档级自定义项的某些方面。

 <xref:Microsoft.VisualStudio.Tools.Applications.Deployment>

 包含 <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> 接口（可实现该接口以便为 Office 解决方案创建 *部署后操作* ）、可能会在安装 Office 解决方案时引发的异常以及其他属于 Visual Studio 基础结构一部分的 API。

 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime>

 包含可以由 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]引发的大多数异常、可以用于在文档级自定义项中缓存数据的多个类以及其他属于 Visual Studio 基础结构一部分的 API。

 <xref:Microsoft.VisualStudio.Tools.Office.BuildTasks>

 包含用于生成 Office 项目的 MSBuild 任务类。

## <a name="see-also"></a>请参阅
- [Visual Studio tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio &#40;中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
