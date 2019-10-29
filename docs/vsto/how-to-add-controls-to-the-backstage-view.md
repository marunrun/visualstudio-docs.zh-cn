---
title: '如何：向 Backstage 视图添加控件 '
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, menus
- controls, Ribbon
- menus, customizing
- Microsoft Office Button
- custom Ribbon, menus
- Ribbon, customizing
- Office button
- Ribbon, menus
- Microsoft Office Menu
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 87cea877928baf52b0442ed9b0d952fcf649f155
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72986013"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>如何：向 Backstage 视图添加控件
  您可以使用功能区设计器将控件添加到单击 "**文件**" 选项卡时打开的菜单。当你运行应用程序时，添加到 "**文件**" 选项卡的控件将显示为名为 "**外接程序**" 的组。

 在 Visual Studio 中使用功能区设计器不能将控件放置在内置控件之前或之后。 内置控件是已在 Backstage 视图中显示的控件。 如果要将控件放置在内置控件之前或之后，必须使用功能区 XML。 有关**功能区（xml）** 的详细信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的详细信息，请参阅面向[开发人员的 office 2010 backstage 视图的简介](/previous-versions/office/developer/office-2010/ee691833(v=office.14))和[为开发人员自定义 office 2010 backstage 视图](/previous-versions/office/developer/office-2010/ee815851(v=office.14))。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>向 Backstage 视图添加控件

1. 在设计视图中打开功能区项。

     有关如何将 "**功能区（可视化设计器）** " 项添加到项目的信息，请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在功能区设计器中，单击 "**文件**" 选项卡。

     此时将显示一个菜单设计器。 此设计图面不包含任何控件。

3. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将以下任意控件拖动到菜单设计器上：

    - Button

    - CheckBox

    - 库

    - 菜单

    - Separator

    - SplitButton

    - ToggleButton

4. 拖动控件，将其移至菜单上的新位置。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
