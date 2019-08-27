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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538091"
---
# <a name="filtering-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的 AddItem 对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当显示**AddItem**嵌套项目，父项目对话框可以控制在对话框中显示的项。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>接口，可以筛选将中的节点**AddItem**对话框。 当子项目显示**AddItem**对话框中，可以实现父`IVsFilterAddProjectItemDlg`本应显示的子项目中的接口和筛选器项。  
  
 当按下特定父项目的函数进行分组的项目时，您可以实现`IVsFilterAddProjectItemDlg`当用户选择**添加项目项**中嵌套项目的快捷菜单上。 实现`IvsFilterAddProjectItemDlg displays`仅项目项或文件特定于该组。 即使它们存储在同一目录中的其他组的项目项被筛选出对话框的。  
  
 当用户在打开**AddItem**对话框中的子级的父项目的实现`IVsFilterAddProjectItemDlg`接口调用。  
  
 `IVsFilterAddProjectItemDlg`接口还可以实现按类别筛选。 有关详细信息，请参阅[将项添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)并[注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [将项添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [嵌套项目](../../extensibility/internals/nesting-projects.md)
