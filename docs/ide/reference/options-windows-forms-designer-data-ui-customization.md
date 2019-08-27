---
title: 选项, Windows 窗体设计器, 自定义数据 UI
ms.date: 08/09/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.WindowsFormsDesigner.Data_UI_Customization
helpviewer_keywords:
- Data UI customization options
- Options dialog box, Windows Forms Designer, Data UI Customization
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ca68a944002d743c6f3d2f89b309b8b77c5dfdb3
ms.sourcegitcommit: 6b0503ed8d25454d6e39a8e606910b3fa58cf1d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "68981683"
---
# <a name="options-dialog-box-windows-forms-designer--data-ui-customization"></a>“选项”对话框：Windows 窗体设计器 > 自定义数据 UI

此对话框定义哪些控件显示在“数据源”窗口中项的可用控件列表中。 若要打开它，请选择“工具”   > “选项”  ，然后选择“Windows 窗体设计器”   > “自定义数据 UI”  。

可以先从“数据源”窗口中的项中选择一个控件，然后将其拖动到 Windows 窗体应用中的窗体。 可用控件由项的数据类型确定。 每个数据类型都有此对话框中定义的有效关联控件列表，包括默认控件。 将项从“数据源”窗口拖动到窗体而不选择控件时，会将所选项的数据类型的默认控件添加到窗体中。

通过选中并清除每个数据类型的可用控件的复选框，自定义关联控件的列表。 若要将控件添加到列表，请将实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> 或 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 数据绑定属性的控件添加到“工具箱”。 然后，控件将出现在数据类型的控件列表中。 有关详细信息，请参阅[如何：向“数据源”窗口添加自定义控件](../..//data-tools/add-custom-controls-to-the-data-sources-window.md)。

## <a name="data-type"></a>数据类型

显示与控件关联的类型列表。 表格表示为 `[List]` 数据类型。 列表示为基础数据存储中列的实际数据类型。

## <a name="associated-controls"></a>关联控件

显示与所选数据类型关联的控件列表。 选择或清除控件旁边的复选框以关联或取消关联。 选定的控件出现在“数据源”窗口中，用于绑定到关联数据类型的数据库列。

## <a name="set-default"></a>设置默认值

将所选控件类型指定为所选数据类型的默认值。 默认控件显示为“数据源”窗口中数据库列的快捷菜单中的第一个选择。 将项从“数据源”窗口拖动到窗体而不选择控件时，会将所选项的数据类型的默认控件添加到窗体中。

只能将一种控件类型指定为数据类型的默认值。

## <a name="clear-default"></a>清除默认值

删除将控件作为所选数据类型默认值的指派。 如果所选数据类型没有默认值，则 `[None]` 将显示为该类型数据库列的快捷菜单中的第一个选择。