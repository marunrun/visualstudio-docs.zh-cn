---
title: 设计 Windows 窗体应用
ms.date: 08/09/2019
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 171cdffa569b342bdbc7dd0da1c8da218e1d622c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589885"
---
# <a name="windows-forms-designer-overview"></a>Windows 窗体设计器概述

Visual Studio 中的 Windows 窗体设计器为创建基于 Windows 窗体的应用程序提供了快速开发解决方案。 借助 Windows 窗体设计器，用户可以轻松地向窗体添加控件，排列这些控件，并针对这些控件的事件编写代码。 有关 Windows 窗体的详细信息，请参阅 [Windows 窗体概述](/dotnet/framework/winforms/windows-forms-overview)。

## <a name="functionality"></a>功能

使用设计器，用户可以：

- 向窗体添加组件、数据控件或基于 Windows 的控件。

- 双击设计器中的窗体并在该窗体的 `Load` 事件中编写代码，或者双击窗体上的控件并针对控件的默认事件编写代码。

- 通过选择控件并键入名称来编辑控件的 Text 属性。

- 通过使用鼠标或箭头键移动所选控件来调整其位置。 同样，使用 Ctrl 和箭头键来更精确地调整位置。 最后，通过使用 Shift 和箭头键来调整控件的大小。

- 通过在单击的同时选择“Shift”或“Ctrl”   来选择多个控件。 使用 Shift  +单击时，选择的第一个控件是对齐或操纵大小时的主导控件。 使用 Ctrl  +单击时，选择的最后一个控件是主导控件，因此主导控件会随着每添加一个新控件而更改。 或者，可以通过拖动要选择的控件周围的选择矩形来选择多个控件。

> [!NOTE]
> 使用 Windows 窗体设计器（而不是“资源编辑器”）更改窗体的资源 (.resx  ) 文件。 如果编辑基于窗体的 .resx 文件，将会看到一个警告，说明在“资源编辑器”中所做的更改可能会丢失。 这是因为 Windows 窗体设计器会生成 .resx 文件。

## <a name="see-also"></a>请参阅

- [Windows 窗体概述](/dotnet/framework/winforms/windows-forms-overview)
- [Windows 窗体控件](/dotnet/framework/winforms/controls/)
- [Windows 窗体中的用户输入](/dotnet/framework/winforms/user-input-in-windows-forms)
- [Windows 窗体中的数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)
- [增强 Windows 窗体应用](/dotnet/framework/winforms/advanced/)
- <xref:System.Windows.Forms?displayProperty=fullName> API 参考
