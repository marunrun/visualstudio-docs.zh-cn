---
title: InfoPath 解决方案
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], InfoPath
- templates [Office development in Visual Studio], InfoPath
- InfoPath [Office development in Visual Studio]
- Office development in Visual Studio, InfoPath solutions
- projects [Office development in Visual Studio], InfoPath
- Office solutions [Office development in Visual Studio], InfoPath
- Office projects [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d227e3c87810156e6e4262a79cfcc9b126d68417
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551740"
---
# <a name="infopath-solutions"></a>InfoPath 解决方案
  Visual Studio 提供了一些项目模板，你可以使用这些模板来创建用于 Microsoft Office InfoPath 2013 和 InfoPath 2010 的 VSTO 外接程序。 InfoPath 在 Office 2016 中不可用。

> [!NOTE]
> 即使已安装 Office 2016, 仍可为 InfoPath 创建 VSTO 外接程序。 只需与 Office 2016 并行安装 InfoPath 2013 或 Office 2013。

 [!INCLUDE[appliesto_infoallapp](../vsto/includes/appliesto-infoallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 InfoPath 的 VSTO 外接程序类似于其他 Microsoft Office 应用程序的 VSTO 外接程序。 这些类型的解决方案包含由应用程序加载的一个程序集。 不管打开了哪个窗体或窗体模板，最终用户都能访问此程序集的功能。 有关 VSTO 外接程序的详细信息, 请参阅 VSTO 外接[程序编程](../vsto/getting-started-programming-vsto-add-ins.md)和[vsto 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)。

> [!NOTE]
> Visual Studio 2015 不包括 Visual Studio 的早期版本中提供的 InfoPath 窗体模板项目。 也无法使用 Visual Studio 2015 打开或编辑用 Visual Studio 的早期版本创建的 InfoPath 窗体模板项目。 但是，可以使用 Visual Studio Tools for Applications 打开和编辑 InfoPath 窗体模板项目。 有关详细信息，请参阅[使用在 InfoPath 2010 的 VSTO 2008 项目](http://go.microsoft.com/fwlink/?LinkID=218903)。

## <a name="automate-infopath-by-using-an-add-in"></a>使用外接程序实现 InfoPath 自动化
 若要从使用 Visual Studio 中的 Office 开发工具创建的 Office VSTO 外接程序访问 InfoPath 对象模型，请在项目中使用 `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回 <xref:Microsoft.Office.Interop.InfoPath.Application> 对象，该对象表示 InfoPath 的当前实例。 有关详细信息, 请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

 从 VSTO 外接程序调入 InfoPath 对象模型时, 将使用在 InfoPath 的主互操作程序集中提供的类型。 该主互操作程序集将作为 VSTO 外接程序中的托管代码和 InfoPath 中的 COM 对象模型之间的桥梁。 InfoPath 主互操作程序集中的所有类型都是在 <xref:Microsoft.Office.Interop.InfoPath> 命名空间中定义的。 有关 InfoPath 主互操作程序集的详细信息, 请参阅[关于 Microsoft Office infopath 主互操作程序集](https://msdn.microsoft.com/1b3ae03c-6951-49e4-a489-4712d3f7ba72)。 有关主互操作程序集的一般详细信息, 请参阅[Office 解决方案&#40;开发&#41;概述 VSTO](../vsto/office-solutions-development-overview-vsto.md)和[office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="customize-the-user-interface-of-infopath-by-using-an-add-in"></a>使用外接程序自定义 InfoPath 的用户界面
 为 InfoPath 创建 VSTO 外接程序时, 有多个不同的 UI 自定义选项。 下表列出了其中一些选项。

|任务|更多相关信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](../vsto/custom-task-panes.md)|
|向 InfoPath 的功能区中添加自定义选项卡。|[自定义 InfoPath 功能区](../vsto/customizing-a-ribbon-for-infopath.md)|

 有关自定义 InfoPath 和其他 Microsoft Office 应用程序的 UI 的详细信息, 请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [关于 Microsoft Office InfoPath 主互操作程序集](https://msdn.microsoft.com/1b3ae03c-6951-49e4-a489-4712d3f7ba72)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [Office 开发中的 InfoPath 2010](http://go.microsoft.com/fwlink/?LinkId=199012)
