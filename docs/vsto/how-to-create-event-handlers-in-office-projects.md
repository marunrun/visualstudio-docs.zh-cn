---
title: 如何：在 Office 项目中创建事件处理程序
description: '了解可为 Visual Basic 和 c # 中的控件创建默认事件处理程序的几种方法。'
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Basic [Office development in Visual Studio], event handlers
- event handlers [Office development in Visual Studio]
- Visual C# [Office development in Visual Studio], event handlers
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f87889c13021a7c0a43b58564210db34301abdf4
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846696"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>如何：在 Office 项目中创建事件处理程序
  可以通过多种方式在 Visual Basic 和 c # 中创建事件处理程序。 在 "设计" 视图中，可以通过双击控件创建控件的默认事件处理程序，也可以使用 " **属性** " 窗口的 "事件" 窗格为控件上的任何事件创建处理程序。 但是，如果在代码视图中，可能不希望切换到设计视图来创建事件处理程序。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>在 Visual Basic 中创建事件处理程序

1. 从 "代码编辑器" 顶部的 " **类名称** " 下拉列表中，选择要为其创建事件处理程序的对象。

    > [!NOTE]
    > 如果要为或创建事件处理程序 `ThisDocument` `ThisWorkbook` ，则必须在 "**类名称**" 下拉列表中选择 **(ThisDocument Events)** 或 **(ThisWorkbook 事件 ")**

2. 从 "代码编辑器" 顶部的 " **方法名称** " 下拉列表中，选择事件。

     Visual Studio 将创建事件处理程序，并将插入点移动到新创建的事件处理程序。 如果事件处理程序已存在，则插入点移动到现有的事件处理程序。

### <a name="to-create-an-event-handler-in-c"></a>在 C 中创建事件处理程序\#

1. 在类的 **启动** 事件中创建事件委托，方法是键入限定的事件名称，后跟一个空格，然后键入，后面 **+=** 不含空格。 例如：

     `this.<object name>.<event name> +=`

2. 在代码行的末尾，按 TAB 键两次。

     Visual Studio 会自动完成代码行，创建事件处理程序，并将插入点移动到新创建的事件处理程序。

## <a name="see-also"></a>请参阅
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
