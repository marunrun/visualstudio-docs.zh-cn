---
title: 项目解决方案
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [Office development in Visual Studio], Project
- Office solutions [Office development in Visual Studio], Project
- Project [Office development in Visual Studio]
- templates [Office development in Visual Studio], Project
- Office projects [Office development in Visual Studio], Project
- solutions [Office development in Visual Studio], Project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f2158918aa6c2487719043abd797eb9d5e8f3f2e
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551394"
---
# <a name="project-solutions"></a>项目解决方案
  [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 提供可用于创建 Microsoft Office Project 的 VSTO 外接程序的项目模板。 VSTO 外接程序可用于自动运行项目、扩展项目功能或自定义项目用户界面 (UI)。

 有关 VSTO 外接程序的详细信息, 请参阅 VSTO 外接[程序编程](../vsto/getting-started-programming-vsto-add-ins.md)和[vsto 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)。如果不熟悉如何与 Microsoft Office 进行编程, 请参阅[Visual &#40;Studio&#41;中的入门 Office 开发](../vsto/getting-started-office-development-in-visual-studio.md)。

 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-project-by-using-the-project-object-model"></a>使用项目对象模型实现项目自动化
 项目对象模型公开了许多可用于实现项目自动化的类型。 可使用这些类型编写代码来完成常规任务，例如以编程方式创建和修改项目中的任务。

 若要从 VSTO 外接程序访问项目对象模型, 请使用`Application`项目中`ThisAddIn`类的字段。 `Application` 字段`Microsoft.Office.Interop.MsProject.Application`返回对象, 该对象表示项目的当前实例。 有关详细信息, 请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

 调入项目对象模型时，将使用项目的主互操作程序集中提供的类型。 该主互操作程序集将作为 VSTO 外接程序中的托管代码和项目中的 COM 对象模型之间的桥梁。 项目主互操作程序集中的所有类型都在 `Microsoft.Office.Interop.MSProject` 命名空间中定义。 有关主互操作程序集的详细信息, 请参阅[Office &#40;解决方案&#41;开发概述 VSTO](../vsto/office-solutions-development-overview-vsto.md)和[office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="use-the-project-object-model-documentation"></a>使用项目对象模型文档
 有关项目对象模型的完整信息，可以参考项目 VBA 对象模型引用。 VBA 对象模型引用在项目对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息, 请参阅[Project 2010 对象模型引用](http://go.microsoft.com/fwlink/?LinkId=199771)。

 VBA 对象模型引用中的所有对象和成员都对应于项目主互操作程序集 (PIA) 中的类型和成员。 例如, VBA 对象模型引用中的 Calendar 对象对应于项目 PIA 中`Microsoft.Office.Interop.MSProject.Calendar`的类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例, 但如果要在创建的项目 VSTO 外接程序项目中使用它们C# , 则必须将本引用中的 VBA 代码转换为 Visual Basic 或视觉对象。使用 Visual Studio。

> [!NOTE]
> 此时，没有任何项目主互操作程序集的参考文档。

### <a name="infrastructure-types-in-the-project-primary-interop-assembly"></a>项目主互操作程序集中的基础结构类型
 编写使用项目 PIA 的代码时，您可能会注意到许多类型在 VBA 参考中都未涉及。 这些附加类型可以帮助将项目的基于 COM 的对象模型中的对象转换为托管代码，而不是在代码中直接使用。

 有关详细信息, 请参阅[Office 主互操作程序集中的类和接口概述](http://go.microsoft.com/fwlink/?LinkId=189592)。

## <a name="customize-the-user-interface-of-project"></a>自定义项目的用户界面
 可以通过下列方式来自定义项目 UI：

|任务|更多相关信息|
|----------|--------------------------|
|向项目的功能区添加自定义选项卡|[功能区概述](../vsto/ribbon-overview.md)|

 有关自定义项目和其他 Microsoft Office 应用程序的 UI 的详细信息, 请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [演练：为项目创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [Office 开发中的 project 2010 和 Project Server 2010](http://go.microsoft.com/fwlink/?LinkId=199016)
