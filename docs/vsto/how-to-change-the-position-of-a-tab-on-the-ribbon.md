---
title: 如何：更改功能区上选项卡的位置
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bf943f9df4499b30e294e4d7e8bf48b25aa52eab
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985990"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>如何：更改功能区上选项卡的位置
  您可以使用 " **Tab 集合编辑器**" 更改功能区上自定义选项卡的顺序。 可以在功能区上的内置选项卡之前或之后放置自定义选项卡。 内置选项卡是 Microsoft Office 应用程序的功能区上已经存在的选项卡。 例如，"**数据**" 选项卡是 Excel 中的内置选项卡。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>更改功能区上选项卡的顺序

1. 在**解决方案资源管理器**中选择功能区代码文件（ *.vb*或 *.cs*文件）。

2. 在 "**视图**" 菜单上，单击 "**设计器**"。

3. 右键单击功能区设计器，然后单击 "**属性**"。

4. 在 "**属性**" 窗口中，选择 "**选项卡**" 属性，然后单击省略号按钮（![ASP.NET mobile 设计器椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）。

     此时将显示 " **Tab 集合编辑器**"。

5. 在 " **Tab 集合编辑器**" 的 "**成员**" 列表中，选择要移动的选项卡，然后单击上箭头或下箭头以更改 tab 键顺序。

### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>将选项卡定位在功能区上的内置选项卡之前或之后

1. 在功能区设计器中，选择一个自定义选项卡。

2. 在 "**属性**" 窗口中，展开 " **ControlId** " 属性，并确保将 " **ControlIdType** " 属性的值设置为 "**自定义**"。

3. 在 "**属性**" 窗口中，展开 "**位置**" 属性。

4. 将**PositionType**属性设置为适当的值：

    - **BeforeOfficeId**将组定位在指定的内置选项卡之前。

    - **AfterOfficeId**将组定位在指定的内置选项卡之后。

5. 将**OfficeId**属性设置为内置选项卡的控件 ID。

     有关控件 Id 的列表，请参阅 [Office 2010 帮助文件：Office 熟知用户界面控件标识符](https://www.microsoft.com/download/details.aspx?id=6627)。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
