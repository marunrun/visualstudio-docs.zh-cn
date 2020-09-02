---
title: PowerPoint 解决方案
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], PowerPoint
- templates [Office development in Visual Studio], PowerPoint
- solutions [Office development in Visual Studio], PowerPoint
- projects [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], PowerPoint
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c41b2942b53c97222abf7308b6706a7cdc734df1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985660"
---
# <a name="powerpoint-solutions"></a>PowerPoint 解决方案
  Visual Studio 提供可用于创建 Microsoft Office PowerPoint 的 VSTO 外接程序的项目模板。 可使用 VSTO 外接程序自动化 PowerPoint、扩展 PowerPoint 功能或自定义 PowerPoint 用户界面 (UI)。

 有关 VSTO 外接程序的详细信息，请参阅 VSTO 外接 [程序编程](getting-started-programming-vsto-add-ins.md) 和 [vsto 外接程序的体系结构](architecture-of-vsto-add-ins.md)。如果不熟悉如何与 Microsoft Office 进行编程，请参阅 [Visual Studio 中的 Office 开发 &#40;入门&#41;](getting-started-office-development-in-visual-studio.md)。

 [!INCLUDE[appliesto_pptallapp](includes/appliesto-pptallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-powerpoint-by-using-the-powerpoint-object-model"></a>使用 PowerPoint 对象模型自动化 PowerPoint
 PowerPoint 对象模型公开了许多你能用于自动化 PowerPoint 的模型。 这些类型使你能够编写代码来完成常规任务：

- 以编程方式创建演示文稿并设置其格式。

- 从演示文稿添加或删除幻灯片。

- 添加或更改幻灯片上的形状。

  若要从 VSTO 外接程序访问 PowerPoint 对象模型，请使用 `Application` `ThisAddIn` 项目中类的字段。 该 `Application` 字段返回一个 [应用程序](/previous-versions/office/developer/office-2010/ff764034(v=office.14)) 对象，该对象表示 PowerPoint 的当前实例。 有关详细信息，请参阅 [PROGRAM VSTO 外接程序](programming-vsto-add-ins.md)。

  调入 PowerPoint 对象模型时，将使用 PowerPoint 的主互操作程序集中提供的类型。 该主互操作程序集充当 VSTO 外接程序中的托管代码与 PowerPoint 中的 COM 对象模型之间的桥梁。 PowerPoint 主互操作程序集中的所有类型都是在 [Microsoft](/previous-versions/office/developer/office-2010/ff763170(v=office.14)) 的命名空间中定义的。 有关主互操作程序集的详细信息，请参阅 [office 解决方案开发概述 &#40;VSTO&#41;](office-solutions-development-overview-vsto.md) 和 [Office 主互操作程序集](office-primary-interop-assemblies.md)。

## <a name="use-the-powerpoint-object-model-documentation"></a><a name="WordOMDocumentation"></a> 使用 PowerPoint 对象模型文档
 有关 PowerPoint 对象模型的完整信息，可以参考 PowerPoint 主互操作程序集 (PIA) 引用和 VBA 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 PowerPoint PIA 参考文档描述了 PowerPoint 的主互操作程序集中的类型。 此文档可从以下位置获取： [PowerPoint 2010 主互操作程序集引用](office-primary-interop-assemblies.md)。

 有关 PowerPoint PIA 设计的详细信息（例如 PIA 中类和接口之间的差异以及如何实现 PIA 中的事件），请参阅 [Office 主互操作程序集中的类和接口的概述](/previous-versions/office/developer/office-2010/ff759900(v=office.14))。

### <a name="vba-object-model-reference"></a>VBA 对象模型引用
 VBA 对象模型引用在 PowerPoint 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅 [PowerPoint 2010 对象模型引用](/office/vba/api/overview/PowerPoint/object-model)。

 VBA 对象模型引用中的所有对象和成员都对应于 PowerPoint 主互操作程序集 (PIA) 中的类型和成员。 例如，VBA 对象模型引用中的表示对象对应于 PowerPoint PIA 中的 [表示](/previous-versions/office/developer/office-2010/ff761925(v=office.14)) 类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果你想要在使用 Visual Studio 创建的 PowerPoint VSTO 外接程序项目中使用它们，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

## <a name="customize-the-user-interface-of-powerpoint"></a>自定义 PowerPoint 的用户界面
 你可以通过以下方式修改 PowerPoint 的 UI。

|任务|更多信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](custom-task-panes.md)|
|向功能区添加自定义选项卡。|[功能区概述](ribbon-overview.md)|
|向功能区上的内置选项卡添加自定义组。|[如何：自定义内置选项卡](how-to-customize-a-built-in-tab.md)|

 有关自定义 PowerPoint 和其他 Microsoft Office 应用程序的 UI 的详细信息，请参阅 [OFFICE UI 自定义](office-ui-customization.md)。

## <a name="see-also"></a>另请参阅
- [演练：创建您的第一个 PowerPoint VSTO 外接程序](walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [VSTO 外接程序编程入门](getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](office-solutions-development-overview-vsto.md)
- [Architecture of VSTO Add-ins](architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](writing-code-in-office-solutions.md)
- [Office 主互操作程序集](office-primary-interop-assemblies.md)
- [Office UI 自定义](office-ui-customization.md)
- [Office 开发中的 PowerPoint 2010](/previous-versions/office/developer/office-2010/ff604967(v=office.14))
