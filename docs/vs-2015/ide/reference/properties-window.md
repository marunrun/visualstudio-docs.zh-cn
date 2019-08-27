---
title: 属性窗口 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio], Properties Window
- handler functions, Properties window
- handlers, Properties window
- Windows messages
- properties [Visual Studio], setting at design time
- properties [Visual Studio], editing
- Property Browser
- Windows messages, adding message handlers
- Properties window, overrides
- virtual functions, Properties window
- Properties window
ms.assetid: e6e0fa4f-75c4-4a52-af15-281cd61876ca
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 582905042938d79a1885279bd19c18f48b49bb84
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438035"
---
# <a name="properties-window"></a>属性窗口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用此窗口可查看和更改编辑器和设计器中选中对象的设计时属性和事件。 还可以使用“属性”窗口编辑和查看文件、项目和解决方案属性。 可以在“视图”菜单上找到“属性”窗口。 可以按 F4 打开它，也可以在“快速启动”窗口中键入“属性”打开。  
  
 “属性”窗口显示不同类型的编辑字段，具体取决于特定属性的需要。 这些编辑字段包括编辑框、下拉列表和自定义编辑器对话框的链接。 以灰色显示的属性为只读属性。  
  
## <a name="uielement-list"></a>UIElement 列表  
 对象名称  
 列出当前选中的对象。 仅来自活动编辑器或设计器的对象可见。 选择多个对象时，仅显示所有选定对象的共同属性。  
  
 按分类顺序  
 按分类列出选中对象的所有属性和属性值。 可以折叠分类以减少可见属性的个数。 展开或折叠分类，类别名称的左侧会显示加号 (+) 或减号 (-)。 按字母顺序列出分类。  
  
 按字母顺序  
 按字母顺序对选中对象的所有设计时属性和事件进行排序。 要编辑不灰显的属性，请单击它右侧的单元格并输入更改内容。  
  
 属性页  
 显示选中项的“属性页”对话框或“项目设计器”。 属性页显示“属性”窗口提供的属性子集、相同属性或属性超集。 使用此按钮查看和编辑与项目的活动配置相关的属性。  
  
 属性  
 显示某个对象的属性。 很多对象的事件还可以使用“属性”窗口查看。  
  
 按属性源排序  
 按源（如继承、应用样式和绑定）对属性进行分组。 仅在设计器中编辑 XAML 文件时可用。  
  
 事件  
 显示对象的事件。  
  
> [!NOTE]
> 该“属性”窗口工具栏控件仅在 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 项目的上下文中的窗体或控件设计器处于活动状态时可用。 编辑 XAML 文件时，事件将显示在属性窗口的单独选项卡上。  
  
 消息  
 列出所有 Windows 消息。 允许针对为选定类提供的消息添加或删除指定处理程序函数。  
  
> [!NOTE]
> 该“属性”窗口工具栏控件仅在“类视图”在 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 项目的上下文中为活动窗口时可用。  
  
 Overrides  
 列出选定类的所有虚函数并允许添加或删除重写函数。  
  
> [!NOTE]
> 该“属性”窗口工具栏控件仅在“类视图”在 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 项目的上下文中为活动窗口时可用。  
  
 说明窗格  
 显示属性类型和属性的简短说明。 可以使用快捷菜单上的说明命令关闭和打开属性的说明。  
  
> [!NOTE]
> 在设计器中编辑 XAML 文件时，此“属性”窗口工具栏控件不可用。  
  
 缩略图视图  
 在设计器中编辑 XAML 文件时，显示了当前所选元素的可视表示形式。  
  
 搜索  
 在设计器中编辑 XAML 文件时提供属性和事件的搜索函数。 搜索框对应于部分单词搜索并在键入时更新搜索结果。  
  
## <a name="see-also"></a>请参阅  
 [项目属性引用](../../ide/reference/project-properties-reference.md)   
 [自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)
