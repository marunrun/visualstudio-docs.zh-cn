---
title: 将 Windows 窗体控件绑定到数据
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 07c5853b673657c3ce8e90467a13bbac3f430b6e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698984"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过将数据绑定到 Windows 窗体，可以向应用程序的用户显示数据。 若要创建这些数据绑定控件，可以将项从**数据源**窗口拖到 Visual Studio 中的 Windows 窗体设计器。 本主题介绍一些最常见的任务、 工具和创建数据绑定 Windows 窗体应用程序时涉及的类。

 ![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png "raddata 数据源拖动操作")

 有关如何在 Visual Studio 中创建数据绑定控件的常规信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 有关在 Windows 窗体中的数据绑定的详细信息，请参阅[Windows 窗体数据绑定](https://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa)。

## <a name="in-this-section"></a>本节内容

- [将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data.md)

- [在保存数据前提交数据绑定控件中正在进行的编辑](../data-tools/commit-in-process-edits-on-data-bound-controls-before-saving-data.md)

- [在 Windows 窗体应用程序中创建查找表](../data-tools/create-lookup-tables-in-windows-forms-applications.md)

- [创建用于搜索数据的 Windows 窗体](../data-tools/create-a-windows-form-to-search-data.md)

- [创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)

- [创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)

- [创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)

- [在窗体间传递数据](../data-tools/pass-data-between-forms.md)

## <a name="bindingsource-component"></a>BindingSource 组件
 <xref:System.Windows.Forms.BindingSource> 组件有两个用途。 首先，你的窗体上的控件绑定到数据时提供一个抽象层。 窗体控件绑定到<xref:System.Windows.Forms.BindingSource>组件 （而不是直接绑定到数据源）。

 其次，它可以管理的对象的集合。 添加到类型<xref:System.Windows.Forms.BindingSource>创建该类型的列表。

 有关详细信息<xref:System.Windows.Forms.BindingSource>组件，请参阅：

- [BindingSource 组件](https://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)

- [BindingSource 组件概述](https://msdn.microsoft.com/library/be838caf-fcb0-4b68-827f-58b2c04b747f)

- [BindingSource 组件体系结构](https://msdn.microsoft.com/library/7bc69c90-8a11-48b1-9336-3adab5b41591)

## <a name="bindingnavigator-control"></a>BindingNavigator 控件
 此组件提供用户界面中进行导航的 Windows 应用程序显示的数据。 有关详细信息，请参阅 [BindingNavigator 控件](https://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e)。

## <a name="datagridview-control"></a>DataGridView 控件
 若要显示和编辑来自许多不同类型的数据源的表格格式数据，请使用<xref:System.Windows.Forms.DataGridView>控件。 您可以将数据绑定到<xref:System.Windows.Forms.DataGridView>通过使用<xref:System.Windows.Forms.DataGridView.DataSource%2A>属性。 有关详细信息，请参阅[DataGridView 控件概述](https://msdn.microsoft.com/library/0a45c661-89dc-4390-9cc6-c47eee501488)。

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
