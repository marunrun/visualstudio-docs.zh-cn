---
title: 在保存前提交数据绑定控件的进程内编辑
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: f0369f4410c1eaf5a168a5291feebf64dbc9ee65
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282704"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>在保存数据前提交数据绑定控件中正在进行的编辑

在数据绑定控件中编辑值时，用户必须导航到当前记录，以将更新后的值提交到控件绑定到的基础数据源。 将项从 "[数据源" 窗口](add-new-data-sources.md)拖到窗体上时，您删除的第一项将在的 "**保存**" 按钮单击事件中生成代码 <xref:System.Windows.Forms.BindingNavigator> 。 此代码将调用的 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法 <xref:System.Windows.Forms.BindingSource> 。 因此， <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 仅为 <xref:System.Windows.Forms.BindingSource> 添加到该窗体的第一个添加了对方法的调用。

<xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）****。

你可以将应用程序配置为自动提交更改，即使在保存过程中，如果用户尝试保存数据但未提交更改，也是如此。

> [!NOTE]
> 设计器 `BindingSource.EndEdit` 只为拖放到窗体上的第一个项添加代码。 因此，你必须添加一行代码来为 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 窗体上的每个调用方法 <xref:System.Windows.Forms.BindingSource> 。 您可以手动添加一行代码，以便为 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 每个调用方法 <xref:System.Windows.Forms.BindingSource> 。 另外，还可以将 `EndEditOnAllBindingSources` 方法添加到窗体中，并在执行保存之前调用它。

下面的代码使用[LINQ （语言集成查询）](/dotnet/csharp/linq/)查询来循环访问所有 <xref:System.Windows.Forms.BindingSource> 组件，并 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 为窗体上的每个组件调用方法 <xref:System.Windows.Forms.BindingSource> 。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>为窗体上的所有 BindingSource 组件调用 EndEdit

1. 将以下代码添加到包含组件的窗体中 <xref:System.Windows.Forms.BindingSource> 。

     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.vb)]

2. 紧靠在任何调用之前添加以下代码行，以便保存窗体的数据（ `TableAdapterManager.UpdateAll()` 方法）：

     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.vb)]

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [分层更新](../data-tools/hierarchical-update.md)
