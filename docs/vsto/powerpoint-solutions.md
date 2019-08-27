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
ms.openlocfilehash: 70968682a8221b88859fd561c9f678aced2911b9
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551468"
---
# <a name="powerpoint-solutions"></a>PowerPoint 解决方案
  Visual Studio 提供可用于创建 Microsoft Office PowerPoint 的 VSTO 外接程序的项目模板。 可使用 VSTO 外接程序自动化 PowerPoint、扩展 PowerPoint 功能或自定义 PowerPoint 用户界面 (UI)。

 有关 VSTO 外接程序的详细信息, 请参阅 VSTO 外接[程序编程](../vsto/getting-started-programming-vsto-add-ins.md)和[vsto 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)。如果不熟悉如何与 Microsoft Office 进行编程, 请参阅[Visual &#40;Studio&#41;中的入门 Office 开发](../vsto/getting-started-office-development-in-visual-studio.md)。

 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 ![视频链接](../vsto/media/playvideo.gif "视频链接")有关相关的视频演示, 请[参阅如何实现:为 Microsoft PowerPoint 创建外接程序？](http://go.microsoft.com/fwlink/?LinkId=132767).

## <a name="automate-powerpoint-by-using-the-powerpoint-object-model"></a>使用 PowerPoint 对象模型自动化 PowerPoint
 PowerPoint 对象模型公开了许多你能用于自动化 PowerPoint 的模型。 这些类型使你能够编写代码来完成常规任务：

- 以编程方式创建演示文稿并设置其格式。

- 从演示文稿添加或删除幻灯片。

- 添加或更改幻灯片上的形状。

  若要从 VSTO 外接程序访问 PowerPoint 对象模型, 请使用`Application`项目中`ThisAddIn`类的字段。 该`Application`字段返回一个[应用程序](/previous-versions/office/developer/office-2010/ff764034(v=office.14))对象, 该对象表示 PowerPoint 的当前实例。 有关详细信息, 请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

  调入 PowerPoint 对象模型时，将使用 PowerPoint 的主互操作程序集中提供的类型。 该主互操作程序集充当 VSTO 外接程序中的托管代码与 PowerPoint 中的 COM 对象模型之间的桥梁。 PowerPoint 主互操作程序集中的所有类型都是在[Microsoft](/previous-versions/office/developer/office-2010/ff763170(v=office.14))的命名空间中定义的。 有关主互操作程序集的详细信息, 请参阅[Office &#40;解决方案&#41;开发概述 VSTO](../vsto/office-solutions-development-overview-vsto.md)和[office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="WordOMDocumentation"></a>使用 PowerPoint 对象模型文档
 有关 PowerPoint 对象模型的完整信息，可以参考 PowerPoint 主互操作程序集 (PIA) 引用和 VBA 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 PowerPoint PIA 参考文档描述了 PowerPoint 的主互操作程序集中的类型。 此文档可从以下位置获得:[PowerPoint 2010 主互操作程序集引用](http://go.microsoft.com/fwlink/?LinkId=189588)。

 有关 PowerPoint PIA 设计的详细信息 (例如 PIA 中类和接口之间的差异以及如何实现 PIA 中的事件), 请参阅[Office 主互操作程序集中的类和接口的概述](http://go.microsoft.com/fwlink/?LinkId=199885)。

### <a name="vba-object-model-reference"></a>VBA 对象模型引用
 VBA 对象模型引用在 PowerPoint 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息, 请参阅[PowerPoint 2010 对象模型引用](http://go.microsoft.com/fwlink/?LinkId=199770)。

 VBA 对象模型引用中的所有对象和成员都对应于 PowerPoint 主互操作程序集 (PIA) 中的类型和成员。 例如, VBA 对象模型引用中的表示对象对应于 PowerPoint PIA 中的[表示](/previous-versions/office/developer/office-2010/ff761925(v=office.14))类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果你想要在使用 Visual Studio 创建的 PowerPoint VSTO 外接程序项目中使用它们，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

## <a name="customize-the-user-interface-of-powerpoint"></a>自定义 PowerPoint 的用户界面
 你可以通过以下方式修改 PowerPoint 的 UI。

|任务|更多相关信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](../vsto/custom-task-panes.md)|
|向功能区添加自定义选项卡。|[功能区概述](../vsto/ribbon-overview.md)|
|向功能区上的内置选项卡添加自定义组。|[如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)|

 有关自定义 PowerPoint 和其他 Microsoft Office 应用程序的 UI 的详细信息, 请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [演练：创建您的第一个 PowerPoint VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [Office 开发中的 PowerPoint 2010](http://go.microsoft.com/fwlink/?LinkId=199015)
