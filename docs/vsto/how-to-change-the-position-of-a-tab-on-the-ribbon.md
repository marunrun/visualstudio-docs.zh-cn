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
ms.openlocfilehash: 512dfda8c95ecd56fe44eb6878e6abc0d942a782
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826727"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>如何：更改功能区上选项卡的位置
  可以通过更改功能区上的自定义选项卡的顺序**Tab 集合编辑器**。 之前或之后在功能区上的内置选项卡，您可以定位自定义选项卡。 内置选项卡是已在 Microsoft Office 应用程序的功能区选项卡。 例如，**数据**选项卡是在 Excel 中的内置选项卡。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>若要更改功能区上选项卡的顺序

1. 选择功能区代码文件 (*.vb*或 *.cs*文件) 中**解决方案资源管理器**。

2. 上**视图**菜单上，单击**设计器**。

3. 右键单击功能区设计器中，然后依次**属性**。

4. 在中**属性**窗口中，选择**选项卡**属性，然后单击省略号按钮 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆"))。

     **Tab 集合编辑器**出现。

5. 在中**Tab 集合编辑器**，在**成员**列表中，选择你想要移动和单击向上或向下箭头可以更改 tab 键顺序选项的卡。

### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>若要定位一个选项卡之前或之后在功能区上的内置选项卡

1. 在功能区设计器中，选择自定义选项卡。

2. 在中**属性**窗口中，展开**ControlId**属性，并请务必的值**ControlIdType**属性设置为**自定义**.

3. 在中**属性**窗口中，展开**位置**属性。

4. 设置**PositionType**属性设置为适当的值：

    - **BeforeOfficeId**定位所指定的内置选项卡之前。

    - **AfterOfficeId**定位所指定的内置选项卡后。

5. 设置**OfficeId**到内置选项卡的控件 ID 的属性。

     控件 Id 的列表，请参阅[Office 2010 帮助文件：Office fluent 用户界面控件标识符](http://go.microsoft.com/fwlink/?LinkID=181052)。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
