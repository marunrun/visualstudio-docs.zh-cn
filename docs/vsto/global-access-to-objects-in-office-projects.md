---
title: 对 Office 项目中对象的全局访问
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ThisDocument_Shutdown
- ThisDocument_Startup
- Globals class, object global access
- worksheets [Office development in Visual Studio], global access
- documents [Office development in Visual Studio], global access
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- application-level addins [Office development in Visual Studio]
- addins [Office development in Visual Studio], events
- workbooks [Office development in Visual Studio], global access
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio]
- Startup event
- Shutdown event
- projects [Office development in Visual Studio], global access
- Office documents [Office development in Visual Studio, global access
- ThisAddin_Startup
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f76a2e74315980764a2cdffe67af4403552de7fe
ms.sourcegitcommit: d293c0e3e9cc71bd4117b6dfd22990d52964addc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2020
ms.locfileid: "88041046"
---
# <a name="global-access-to-objects-in-office-projects"></a>对 Office 项目中对象的全局访问
  创建 Office 项目时，Visual Studio 将在项目中自动生成一个名为 `Globals` 的类。 可以使用 `Globals` 类在运行时从项目中的任何代码访问多个不同的项目项。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="how-to-use-the-globals-class"></a>如何使用 Globals 类
 `Globals` 是一个静态类，该类将对某些项的引用保留在你的项目中。 通过使用 `Globals` 类，可在运行时从项目中的任何代码访问以下各项：

- Excel 工作簿或模板项目中的 `ThisWorkbook` 和 `Sheet`*n* 类。 可以通过使用 `Globals.ThisWorkbook` 和 `Sheet`*n* 属性访问这些对象。

- Word 文档或模板项目中的 `ThisDocument` 类。 可以通过使用 `Globals.ThisDocument` 属性访问此对象。

- `ThisAddIn`VSTO 外接程序项目中的类。 可以通过使用 `Globals.ThisAddIn` 属性访问此对象。

- 项目中通过使用功能区设计器自定义的所有功能区。 可以通过使用 `Globals.Ribbons` 属性访问功能区。 有关详细信息，请参阅[在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)。

- Outlook VSTO 外接程序项目中的所有 Outlook 窗体区域。 可以通过使用 `Globals.FormRegions` 属性访问这些窗体区域。 有关详细信息，请参阅[在运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)。

- 一个工厂对象，该对象使你可在运行时在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]的项目中创建功能区控件和主机项。 可以通过使用 `Globals.Factory` 属性访问此对象。 此对象是实现以下接口之一的类的实例：

  - [Microsoft。](xref:Microsoft.Office.Tools.Factory)

  - ["Microsoft"。](xref:Microsoft.Office.Tools.Excel.Factory)

  - ["Microsoft"。](xref:Microsoft.Office.Tools.Outlook.Factory)

  - [Microsoft. Tools。](xref:Microsoft.Office.Tools.Word.Factory)

  例如，当用户单击 Excel 的文档级项目中的操作窗格上的按钮时，你可以使用 `Globals.Sheet1` 属性将文本插入到 <xref:Microsoft.Office.Tools.Excel.NamedRange> 上的 `Sheet1` 控件中。

  [!code-vb[Trin_VstcoreProgramming#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#1)]
  [!code-csharp[Trin_VstcoreProgramming#1](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs#1)]

 `Globals`在初始化文档或 VSTO 外接程序之前，尝试使用类的代码可能会引发运行时异常。 例如，声明一个类级变量时使用 `Globals` 可能会失败，因为在对声明的对象进行实例化之前，可能不会使用对所有主机项的引用将 `Globals` 类初始化。

> [!NOTE]
> 永远不会在设计时初始化 `Globals` 类，控件实例由设计器创建。 这意味着，如果您在用户控件类的内部创建使用类的属性的用户控件 `Globals` ，则在尝试使用返回的对象之前，必须检查属性是否返回**null** 。

## <a name="see-also"></a>另请参阅
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [在运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [文档宿主项](../vsto/document-host-item.md)
- [工作簿宿主项](../vsto/workbook-host-item.md)
- [工作表宿主项](../vsto/worksheet-host-item.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
