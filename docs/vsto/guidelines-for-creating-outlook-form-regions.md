---
title: Outlook 窗体区域创建准则
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], guidelines
- icons [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d48a3ad24d094d0ebc822b572f2521eaefae5356
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826491"
---
# <a name="guidelines-to-create-outlook-form-regions"></a>若要创建 Outlook 窗体区域的准则
  以下信息可以帮助优化窗体区域和避免潜在问题。

- [使用窗体区域名称](#UsingFormRegions)。

- [禁用窗体区域继承](#DisablingInheritance)。

- [了解类型和消息的类名](#ClassNames)。

- [设计相邻窗体区域为阅读窗格](#ReadingPane)。

- [使用最佳图标大小](#UsingOptimal)。

  有关窗体区域的详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

  [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="UsingFormRegions"></a> 使用窗体区域名称
 用来描述窗体区域的名称有多个。 请务必了解这些名称之间的区别以及它们如何影响窗体区域。 下表对每个名称进行了描述。

|窗体区域名称|描述|
|----------------------|-----------------|
|窗体区域项名称|你在“添加新项”  对话框中为“Outlook 窗体区域”  项指定的名称。 这是将在“解决方案资源管理器” 中显示的窗体区域代码文件的名称。|
|<xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> 属性|你在  “新建 Outlook 窗体区域”向导的  “提供说明性文本并选择显示首选项”页中指定此名称。 此名称作为  “属性”窗口中的 **FormRegionName** 属性显示。<br /><br /> 使用 <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> 属性指定用于在 Outlook 用户界面 (UI) 标识窗体区域的标签。 对于单独的窗体区域，此名称显示为 Outlook 项目功能区上的按钮。<br /><br /> 对于相邻的窗体区域，此名称显示为窗体区域上方的标题文本。|
|`Microsoft.Office.Tools.Outlook.FormRegionName` 属性|当你向项目添加  “Outlook 窗体区域”项时，Visual Studio 将此属性设置为窗体区域的完全限定名。 默认完全限定名的格式是：VSTO 外接程序的名称加点号加窗体区域，例如 `OutlookAddIn1.FormRegion1`。<br /><br /> 此完全限定名也作为窗体区域工厂类顶部的一个属性显示。<br /><br /> `Microsoft.Office.Tools.Outlook.FormRegionName` 属性用于唯一标识跨所有 Outlook VSTO 外接程序的窗体区域。不能通过重命名窗体区域项或更改 <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> 属性来更改 `Microsoft.Office.Tools.Outlook.FormRegionName` 属性的值。 若要更改此名称，必须在窗体区域代码文件中修改 `Microsoft.Office.Tools.Outlook.FormRegionName` 属性。|

## <a name="DisablingInheritance"></a> 禁用窗体区域继承
 默认情况下，自定义 message 类继承 message 基类的所有窗体区域关联。 例如，名为 `IPM.Task.Contoso` 的 message 类派生自 `IPM.Task`。 因此，`IPM.Task.Contoso` 继承 `IPM.Task` 的窗体区域关联。

 如果不希望窗体区域与任何派生的 message 类关联，将窗体区域的 <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ExactMessageClass%2A> 属性设置为 **true**。 例如，如果将一个相邻的窗体区域与相关联`IPM.Task`并设置<xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ExactMessageClass%2A>属性设置为**true**，窗体区域只会追加到标准任务窗体的底部。 窗体区域不会追加到任何自定义版本的标准任务窗体的底部。

## <a name="ClassNames"></a> 了解类型和 message 类名称
 Outlook 项目的类型名称与 Outlook 项目的 message 类名称不同。 例如，RSS 项的类型名称是 `Microsoft.Office.Interop.Outlook.PostItem`， 而 RSS 项的 message 类名是 `IPM.Post.RSS`。

 使用类型名称可在代码中引用 Outlook 项目。 类型名称的列表，请参阅[将窗体区域与 Outlook 消息类相关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)。

 在  “新建 Outlook 窗体区域”向导中使用 Outlook 项目的 message 类名可将该项目与窗体区域关联。 有关有效 message 类名的列表，请参阅[将窗体区域与 Outlook 消息类相关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)。

## <a name="ReadingPane"></a> 为阅读窗格设计相邻窗体区域
 可以使用 Outlook 阅读窗格在不打开 Outlook 项目的情况下预览项目。 阅读窗格为只读。 因此，项目和窗体区域在阅读窗格中打开时，添加到相邻窗体区域（例如文本框）的输入控件可能不像预期那样工作。

 例如，如果具有相邻窗体区域的项目在阅读窗格中打开，可能出现以下情况：

1. 选择文本框中位于窗体区域的部分文本。

2. 按**删除**。

3. 整个邮件项将删除，而不是在文本框中的文本。

   如果正在设计的相邻窗体区域包含输入控件，请在阅读窗格中测试控件以确保它们工作正常。 请考虑添加禁用不像预期那样工作的控件的自定义代码。

   或者，可以将窗体区域的 <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ShowInspectorRead%2A> 属性设置为 **False**。 这样，窗体区域就无法在阅读窗格中使用。

## <a name="UsingOptimal"></a> 使用最佳图标大小
 你可以在  “属性”窗口的  “图标”属性组设置图标属性，指定希望窗体区域显示哪些图标。 遵循以下准则以实现最佳的视觉质量：

- 对于 **页面** 图标，使用可移植网络图形 (PNG) 文件。

- **窗口** 图标应为 32 x 32 像素。

- 所有其他图标应为 16 x 16 像素。

  对于具有 Separate、Replace 或 ReplaceAll 窗体区域的项， **页面** 图标显示在项检查器的功能区中。

  **窗口**图标将出现在通知区域，然后在**Alt**+**选项卡**打开的对话框中的项的显示替换或全部替换窗体区域。

## <a name="see-also"></a>请参阅
- [访问在运行时的窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [将窗体区域与 Outlook 消息类相关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
