---
title: 在保存前提交数据绑定控件的进程内编辑
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- committing edited records
- data-bound controls, in-process edits
- DataBinding class, committing edited records
- hierarchical update, committing edited records
- BindingSource class, committing edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4a708128f827568e072c617effff17129e41e558
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586934"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>在保存数据前提交数据绑定控件中正在进行的编辑

在数据绑定控件中编辑值时，用户必须导航到当前记录，以将更新后的值提交到控件绑定到的基础数据源。 将项从 "[数据源" 窗口](add-new-data-sources.md)拖到窗体上时，所放置的第一项将在 <xref:System.Windows.Forms.BindingNavigator>的 "**保存**" 按钮单击事件中生成代码。 此代码将调用 <xref:System.Windows.Forms.BindingSource>的 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法。 因此，仅为添加到窗体的第一个 <xref:System.Windows.Forms.BindingSource> 生成对 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法的调用。

<xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。

你可以将应用程序配置为自动提交更改，即使在保存过程中，如果用户尝试保存数据但未提交更改，也是如此。

> [!NOTE]
> 设计器仅为拖放到窗体上的第一个项添加 `BindingSource.EndEdit` 代码。 因此，你必须添加一行代码来为窗体上的每个 <xref:System.Windows.Forms.BindingSource> 调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法。 您可以手动添加一行代码，以便为每个 <xref:System.Windows.Forms.BindingSource>调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法。 或者，您可以将 `EndEditOnAllBindingSources` 方法添加到窗体中，然后在执行保存之前调用它。

下面的代码使用[LINQ （语言集成查询）](/dotnet/csharp/linq/)查询来循环访问所有 <xref:System.Windows.Forms.BindingSource> 组件，并为窗体上的每个 <xref:System.Windows.Forms.BindingSource> 调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>为窗体上的所有 BindingSource 组件调用 EndEdit

1. 将以下代码添加到包含 <xref:System.Windows.Forms.BindingSource> 组件的窗体中。

     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.vb)]

2. 直接在任何调用之前添加以下代码行，以便保存窗体的数据（`TableAdapterManager.UpdateAll()` 方法）：

     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.vb)]

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [分层更新](../data-tools/hierarchical-update.md)
