---
title: 如何：向功能区组添加对话框启动器
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 29b260929d0478749296496db5b454326497d3ad
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541613"
---
# <a name="how-to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>如何：向功能区组添加对话框启动器
  您可以向功能区上的任何组添加对话框启动器。 对话框启动器是出现在组中的小图标。 用户单击此图标可打开相关对话框或任务窗格，其中提供了与组相关的更多选项。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>向功能区组添加对话框启动器

1. 在**解决方案资源管理器**中选择功能区代码文件（*.vb*或 *.cs*文件）。

2. 在 "**视图**" 菜单上，单击 "**设计器**"。

3. 在功能区设计器中，右键单击任何组，然后单击 "**添加 DialogBoxLauncher**"。

     将代码添加到 <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick> 组的事件，以打开自定义或内置对话框。

## <a name="see-also"></a>请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：向 backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：在运行时更新功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
