---
title: 筛选嵌套项目的 AddItem 对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc3ff1f85e8c8c71bf8ef16e6fe0c89bf3613f4d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328953"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的 AddItem 对话框
当显示**AddItem**嵌套项目，父项目对话框可以控制在对话框中显示的项。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>接口，可以筛选将中的节点**AddItem**对话框。 当子项目显示**AddItem**对话框中，可以实现父`IVsFilterAddProjectItemDlg`本应显示的子项目中的接口和筛选器项。

 当按下特定父项目的函数进行分组的项目时，您可以实现`IVsFilterAddProjectItemDlg`当用户选择**添加项目项**中嵌套项目的快捷菜单上。 实现`IvsFilterAddProjectItemDlg displays`仅项目项或文件特定于该组。 即使它们存储在同一目录中的其他组的项目项被筛选出对话框的。

 当用户在打开**AddItem**对话框中的子级的父项目的实现`IVsFilterAddProjectItemDlg`接口调用。

 `IVsFilterAddProjectItemDlg`接口还可以实现按类别筛选。 有关详细信息，请参阅[将项添加到添加新项对话框中](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)并[注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [将项目添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)