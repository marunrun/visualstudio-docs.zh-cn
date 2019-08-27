---
title: 如何：将对话框启动器添加到功能区组
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- dialog box launcher [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], dialog box launcher
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9d831cb629665e641394d011bd11eb74481c4f94
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826439"
---
# <a name="how-to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>如何：将对话框启动器添加到功能区组
  您可以向功能区上的任何组添加对话框启动器。 对话框启动器是一组中出现一个小图标。 用户单击此图标可打开相关的对话框或提供更多与该组相关的选项的任务窗格。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>若要将对话框启动器添加到功能区组

1. 选择功能区代码文件 (*.vb*或 *.cs*文件) 中**解决方案资源管理器**。

2. 上**视图**菜单上，单击**设计器**。

3. 在功能区设计器中，右键单击任意组，然后单击**添加 DialogBoxLauncher**。

     将代码添加到<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick>要打开自定义或内置对话框中的组的事件。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [如何：导出功能区从功能区设计器功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：将控件添加到 backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [为 Outlook 中自定义功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：更新在运行时功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
