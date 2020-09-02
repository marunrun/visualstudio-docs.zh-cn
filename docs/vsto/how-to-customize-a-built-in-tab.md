---
title: 如何：自定义内置选项卡
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- built-in tabs [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5f73ec7a8555a5e5d569d4316ca619747550bf11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547181"
---
# <a name="how-to-customize-a-built-in-tab"></a>如何：自定义内置选项卡
  可以将组和控件添加到内置选项卡。内置选项卡是 Microsoft Office 应用程序的功能区上已有的选项卡。 例如，" **数据** " 选项卡是 Excel 中的内置选项卡。 创建自定义组时，它显示在选项卡末尾，但可以在选项卡上任意移动你的组。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> 可以将组添加到内置选项卡，但不能删除内置选项卡中的内置组。

### <a name="to-add-groups-to-a-built-in-tab"></a>将组添加到内置选项卡

1. 在 **解决方案资源管理器**中右键单击功能区代码文件，然后单击 " **视图设计器**"。

    > [!NOTE]
    > 如果功能区代码文件未出现在 **解决方案资源管理器**中，则必须将 **功能区项** 添加到项目。 请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 右键单击功能区设计器中的任意选项卡，然后单击 " **属性**"。

3. 在 " **属性** " 窗口中，展开 " **ControlId** " 属性，然后将 " **ControlIdType** " 属性设置为 " **Office**"。

4. 将 **OfficeId** 属性设置为要自定义的内置选项卡的 *控件 ID* 。

     控件 ID 是唯一标识 Microsoft Office 应用程序中内置的选项卡、组和控件的名称。

     有关控件 Id 的列表，请参阅 [office 2010 帮助文件： office 熟知用户界面控件标识符](https://www.microsoft.com/download/details.aspx?id=6627)。

5. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将 "组" 拖到选项卡上。

    > [!NOTE]
    > 设计器中不显示内置组。 因此，确定是否使用内置选项卡的唯一方法是检查该选项卡的 " **ControlId** " 属性。

### <a name="to-position-groups-on-a-built-in-tab"></a>若要在内置选项卡上定位组

1. 在“功能区设计器”中，选择自定义组。

2. 在 " **属性** " 窗口中，展开 " **位置** " 属性。

3. 将 **PositionType** 属性设置为适当的值：

    - **BeforeOfficeId** 将组定位在指定的内置组之前。

    - **AfterOfficeId** 将组定位在指定的内置组之后。

4. 将 **OfficeId** 属性设置为内置组的控件 ID。

     有关控件 Id 的列表，请参阅 [office 2010 帮助文件： office 熟知用户界面控件标识符](https://www.microsoft.com/download/details.aspx?id=6627)。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
