---
title: 筛选嵌套项目的"添加项目"对话框 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2bc97b6041f4844ff71fe1d38a7103e1219888be
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708382"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的"添加项目"对话框
当您为嵌套项目显示 **"添加项目"** 对话框时，父项目可以控制对话框中显示的项目。

 该<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>接口允许您筛选将在 **"添加项目"** 对话框中的节点。 当子项目显示 **"添加项目**"对话框时，父项可以实现`IVsFilterAddProjectItemDlg`接口和筛选器项，否则这些项将显示在子项的项目中。

 当项目按特定父项目下的函数分组时，可以在用户选择嵌套`IVsFilterAddProjectItemDlg`项目中的快捷菜单上**添加项目项**时实现。 仅`IvsFilterAddProjectItemDlg displays`实现特定于该组的项目项或文件。 其他组的项目项从对话框中筛选出来，即使它们存储在同一目录中也是如此。

 当用户为子级打开 **"添加项目**"对话框时，将调用父项目的`IVsFilterAddProjectItemDlg`接口实现。

 接口`IVsFilterAddProjectItemDlg`还可以按类别实现筛选。 有关详细信息，请参阅[将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)和[注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
