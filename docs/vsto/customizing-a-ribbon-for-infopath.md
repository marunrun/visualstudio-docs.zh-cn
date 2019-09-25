---
title: 自定义 InfoPath 功能区
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- InfoPath [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76ec069ef71890a69fdbd41f40bd91cf75d93cd4
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255508"
---
# <a name="customize-a-ribbon-for-infopath"></a>自定义 InfoPath 功能区
  在 Microsoft Office InfoPath 中自定义功能区时，必须考虑自定义功能区在应用程序中出现的位置。 [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)] 可以在以下三种类型的 InfoPath 应用程序窗口中显示功能区：

- 显示在设计模式下打开的窗体模板的窗口。

- 显示基于窗体模板的窗体的窗口。

- “打印预览”窗口。

  **适用于:** 本主题中的信息适用于 InfoPath 2010 的 VSTO 外接程序项目。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

  用户和设计人员在设计模式下打开一个窗体模板，以修改该模板的外观和布局。 用户打开基于窗体模板的窗体，以添加内容。

  通过“打印预览”窗口，设计人员和用户可以在打印窗体或窗体模板页面之前进行预览。

> [!NOTE]
> “打印预览”窗口中不显示 “外接程序”选项卡。 如果希望“打印预览”窗口中显示一个自定义选项卡，请确保该选项卡的“OfficeId” 属性未设置成“TabAddIns”。

 必须为希望在其中显示功能区的每个窗口指定功能区类型。

## <a name="specify-the-ribbon-type-in-the-ribbon-designer"></a>在功能区设计器中指定功能区类型
 如果使用的是 "**功能区（可视化设计器）** " 项，请在 "**属性**" 窗口中单击功能区的 " **RibbonType** " 属性，然后选择下表中所述的任何功能区 id。

|功能区 ID|运行项目时将在其中显示功能区的窗口|
|---------------|---------------------------------------------------------------------|
|**Microsoft.InfoPath.Designer**|显示在设计模式下打开的窗体模板的窗口。|
|**Microsoft.InfoPath.Designer**|显示基于窗体模板的窗体的窗口。|
|**Microsoft.InfoPath.Designer**|“打印预览”窗口。|

 你可以向项目添加多个功能区。 如果多个功能区共享一个功能区 ID，请重写项目的 `ThisAddin` 类中的 `CreateRibbonExtensibilityObject` 方法，以指定要在运行时显示的功能区。 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>使用功能区 XML 指定功能区类型
 如果使用的是 "**功能区（XML）** " 项，请检查<xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A>方法中的*ribbonID*参数的值，并返回相应的功能区。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> 方法由 Visual Studio 在功能区代码文件中自动生成。 *ribbonID* 参数是一个字符串，标识当前打开的 InfoPath 窗口的类型。

 下面的代码示例演示如何仅在显示在设计模式下打开的窗体模板的窗口中显示自定义功能区。 要显示的功能区在 `GetResourceText()` 方法中指定，该方法在功能区类中生成。 有关功能区类的详细信息，请参阅 [Ribbon XML](../vsto/ribbon-xml.md)。

 [!code-csharp[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/CSharp/myinfopathproject/ribbon.cs#1)]
 [!code-vb[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/VisualBasic/myinfopathproject/ribbon.vb#1)]

## <a name="see-also"></a>请参阅
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
