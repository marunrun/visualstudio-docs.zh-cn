---
title: '如何：将控件添加到 Backstage 视图 '
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
ms.openlocfilehash: c4241464fe8a43af882fbdbad0f898838e8fd897
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826776"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>如何：将控件添加到 Backstage 视图
  可以使用功能区设计器将控件添加到单击时打开的菜单**文件**选项卡。当运行该应用程序，您将添加到的控件**文件**选项卡显示名为的组**外接程序**。

 使用 Visual Studio 中的功能区设计器，无法在内置控件前后放置控件。 内置控件是已出现在 Backstage 视图中的控件。 如果你想要在内置控件前后放置控件，必须使用功能区 XML。 有关详细信息**功能区 (XML)**，请参阅[功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的详细信息，请参阅[开发人员的 Office 2010 Backstage 视图简介](http://go.microsoft.com/fwlink/?LinkId=182189)并[自定义开发人员的 Office 2010 Backstage 视图](http://go.microsoft.com/fwlink/?LinkId=182188)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>若要将控件添加到 Backstage 视图

1. 在设计视图中打开功能区项。

     有关如何添加**功能区 （可视化设计器）** 到你的项目项，请参阅[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在功能区设计器中，单击**文件**选项卡。

     菜单设计器随即出现。 此设计图面上不包含任何控件。

3. 从**Office 功能区控件**选项卡**工具箱**，将任何以下控件拖动到菜单设计器上：

    - Button

    - CheckBox

    - 库

    - 菜单

    - Separator

    - SplitButton

    - ToggleButton

4. 将控件的菜单上将其移动到新位置。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
