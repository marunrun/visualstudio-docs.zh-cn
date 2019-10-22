---
title: 在运行时访问窗体区域
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Explorers [Office development in Visual Studio]
- form regions [Office development in Visual Studio], accessing at run time
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5dd8818b57a1aa33b70254303150d8f00e36cc02
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255801"
---
# <a name="access-a-form-region-at-run-time"></a>在运行时访问窗体区域

|适用对象|
|----------------|
|本主题中的信息仅适用于以下项目类型和 Microsoft Office 版本。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。<br /><br /> **项目类型**<br /><br /> -VSTO 外接程序项目<br /><br /> **Microsoft Office 版本**<br /><br /> -   [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]|

 使用 `Globals` 类可以从 Outlook 项目中的任何位置访问窗体区域。 有关`Globals`类的详细信息，请参阅[对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="access-form-regions-that-appear-in-a-specific-outlook-inspector-window"></a>访问在特定 Outlook 检查器窗口中显示的窗体区域
 若要访问在特定 Outlook 检查器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性，并传入一个表示该检查器的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象。

 下面的示例获取在当前获得焦点的检查器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的集合中的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 [!code-vb[Trin_Outlook_FR_Access#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#2)]
 [!code-csharp[Trin_Outlook_FR_Access#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#2)]

## <a name="access-form-regions-that-appear-in-a-specific-outlook-explorer-window"></a>访问在特定 Outlook 资源管理器窗口中显示的窗体区域
 若要访问在特定 Outlook 资源管理器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性，并传入一个表示该资源管理器的 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象。

 下面的示例获取在当前获得焦点的资源管理器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的集合中的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 [!code-vb[Trin_Outlook_FR_Access#3](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#3)]
 [!code-csharp[Trin_Outlook_FR_Access#3](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#3)]

## <a name="access-all-form-regions"></a>访问所有窗体区域
 若要访问在所有资源管理器和所有检查器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性。

 下面的示例获取在所有资源管理器和所有检查器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 [!code-vb[Trin_Outlook_FR_Access#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Access#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#1)]

## <a name="access-controls-on-a-form-region"></a>访问窗体区域中的控件
 若要使用 `Globals` 类来访问窗体区域中的控件，必须使窗体区域代码文件外部的代码可以访问控件。

### <a name="form-regions-designed-in-the-form-region-designer"></a>在窗体区域设计器中设计的窗体区域
 对于 C#，更改要访问的每个控件的修饰符。 若要执行此操作，请在窗体区域设计器中选择每个控件，然后在“属性” 窗口中将“Modifiers” 属性更改为“Internal” 或“public” 。 例如，如果将 **的“Modifier”** `textBox1` 属性更改为“Internal”，则可以通过键入 `textBox1` 来访问 `Globals.FormRegions.FormRegion1.textBox1`。

 对于 Visual Basic，不需要更改修饰符。

### <a name="imported-form-regions"></a>导入的窗体区域
 如果导入在 Outlook 中设计的窗体区域，则窗体区域中每个控件的访问修饰符变为专用。 因为无法使用窗体区域设计器来修改导入的窗体区域，所以无法在“属性” 窗口更改控件的修饰符。

 若要能够从窗体区域代码文件外部访问控件，请在窗体区域代码文件中创建属性来返回该控件。

 有关如何在中C#创建属性的详细信息，请[参阅如何：声明和使用读写属性&#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties)。

 有关如何在 Visual Basic 中创建属性的详细信息，请[参阅如何：创建属性（Visual Basic）](/dotnet/visual-basic/programming-guide/language-features/procedures/how-to-create-a-property)。

## <a name="see-also"></a>请参阅
- [创建 Outlook 窗体区域的准则](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [Outlook 窗体区域中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
- [将窗体区域与 Outlook 邮件类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [如何：阻止 Outlook 显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
