---
title: 筛选嵌套项目的 AddItem 对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7bb98eac2bc481aa5e3652144dfbcadf70430d04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538091"
---
# <a name="filtering-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的 AddItem 对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当你为嵌套项目显示 **AddItem** 对话框时，父项目可以控制哪些项显示在对话框中。  
  
 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> 接口可以筛选将在 **AddItem** 对话框中的节点。 当子项目显示 " **AddItem** " 对话框时，父级可以实现 `IVsFilterAddProjectItemDlg` 接口，并筛选将在子项的项目中显示的项。  
  
 当项目按特定父项目中的函数分组后，可以在 `IVsFilterAddProjectItemDlg` 用户在嵌套项目的快捷菜单上选择 " **添加项目项** " 时实现。 `IvsFilterAddProjectItemDlg displays`仅实现特定于该组的项目项或文件。 其他组的项目项将从对话框筛选出来，即使它们存储在同一目录中也是如此。  
  
 当用户打开儿童的 **AddItem** 对话框时，将调用该接口的父项目的实现 `IVsFilterAddProjectItemDlg` 。  
  
 `IVsFilterAddProjectItemDlg`接口还可以实现按类别筛选。 有关详细信息，请参阅向 ["添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) 和 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [嵌套项目](../../extensibility/internals/nesting-projects.md)
