---
title: 为 Outlook 中自定义功能区
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], Ribbon
- customizing the Ribbon, about customizing the Ribbon
- custom Ribbon, about customizing the Ribbon
- Ribbon [Office development in Visual Studio], Outlook
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 58735a36afd48132f919e370da5e27fd0c42a0f0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62956144"
---
# <a name="customize-a-ribbon-for-outlook"></a>为 Outlook 中自定义功能区
  在 Microsoft Office Outlook 中自定义功能区时，必须考虑自定义功能区在应用程序中出现的位置。 在主应用程序用户界面 (UI) 和用户执行某些任务（例如创建电子邮件消息）时打开的窗口中，Outlook 会显示功能区。 这些应用程序窗口被命名为检查器。

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：使用功能区设计器自定义 Outlook 功能区中？](http://go.microsoft.com/fwlink/?LinkID=130312).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>将自定义功能区添加到主应用程序 UI
 主应用程序 UI 在 Outlook 中被称为资源管理器。 如果使用的**功能区 （可视化设计器）** 项，您可以将功能区添加到资源管理器通过单击**RibbonType**属性中的功能区**属性**窗口中，然后选择**Microsoft.Outlook.Explorer**。

## <a name="assign-a-ribbon-to-an-inspector"></a>将功能区分配给检查器
 通过指定与该检查器 message 类相对应的功能区类型来确定要进行自定义的检查器。

 如果使用的**功能区 （可视化设计器）** 项，单击**RibbonType**属性中的功能区**属性**窗口中，并选择一个或多个功能区 Id值的列表。

 可以向项目添加多个功能区。 如果多个功能区共享一个功能区 ID，请重写项目的 `ThisAddin` 类中的 `CreateRibbonExtensibilityObject` 方法，以指定要在运行时显示的功能区。 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。 有关每个功能区类型的详细信息，请参阅技术文章[自定义 Outlook 2007 中的功能区](/previous-versions/office/developer/office-2007/bb226712(v=office.12))。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>使用功能区 XML 指定功能区类型
 如果使用的**功能区 (XML)** 项，请检查的值*ribbonID*中的参数<xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A>方法并返回相应的功能区。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> 方法由 Visual Studio 在功能区代码文件中自动生成。 *RibbonID*参数是用于标识资源管理器或检查器的特定类型的字符串。 有关的可能值的完整列表*ribbonID*参数，请参阅技术文章[自定义 Outlook 2007 中的功能区](/previous-versions/office/developer/office-2007/bb226712(v=office.12))。

 以下代码示例演示如何仅在 `Microsoft.Outlook.Mail.Compose` 检查器中显示自定义功能区。 这是用户创建新的电子邮件时将打开的检查器。 中指定要显示功能区`GetResourceText()`方法中生成**功能区**类。 有关详细信息**功能区**类，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

 [!code-csharp[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs#1)]
 [!code-vb[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb#1)]

## <a name="see-also"></a>请参阅
- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
