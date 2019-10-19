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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8a03f4df57b216fa68e5ac24df80b67917aa3e3f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672987"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将数据绑定到 Windows 窗体来向应用程序的用户显示数据。 若要创建这些数据绑定控件，可以将项从 "**数据源**" 窗口拖动到 Visual Studio 中的 Windows 窗体设计器。 本主题介绍创建数据绑定 Windows 窗体应用程序所涉及的一些最常见的任务、工具和类。

 ![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png "raddata 数据源拖动操作")

 有关如何在 Visual Studio 中创建数据绑定控件的一般信息，请参阅[在 Visual studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 有关 Windows 窗体中的数据绑定的详细信息，请参阅[Windows 窗体数据绑定](https://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa)。

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
 <xref:System.Windows.Forms.BindingSource> 组件有两个用途。 首先，在将窗体上的控件绑定到数据时，它提供抽象层。 窗体上的控件绑定到 <xref:System.Windows.Forms.BindingSource> 组件（而不是直接绑定到数据源）。

 其次，它可以管理对象的集合。 将类型添加到 <xref:System.Windows.Forms.BindingSource> 会创建该类型的列表。

 有关 <xref:System.Windows.Forms.BindingSource> 组件的详细信息，请参阅：

- [BindingSource 组件](https://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)

- [BindingSource 组件概述](https://msdn.microsoft.com/library/be838caf-fcb0-4b68-827f-58b2c04b747f)

- [BindingSource 组件体系结构](https://msdn.microsoft.com/library/7bc69c90-8a11-48b1-9336-3adab5b41591)

## <a name="bindingnavigator-control"></a>BindingNavigator 控件
 此组件提供一个用户界面，用于浏览 Windows 应用程序所显示的数据。 有关详细信息，请参阅 [BindingNavigator 控件](https://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e)。

## <a name="datagridview-control"></a>DataGridView 控件
 若要显示和编辑多种不同类型的数据源中的表格数据，请使用 <xref:System.Windows.Forms.DataGridView> 控件。 使用 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性可以将数据绑定到 <xref:System.Windows.Forms.DataGridView>。 有关详细信息，请参阅[DataGridView 控件概述](https://msdn.microsoft.com/library/0a45c661-89dc-4390-9cc6-c47eee501488)。

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
