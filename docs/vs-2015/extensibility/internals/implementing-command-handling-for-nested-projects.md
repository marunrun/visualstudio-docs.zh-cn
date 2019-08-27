---
title: 实现命令的处理嵌套项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2fbce80b2e8c337eddf0d34954a7fd70b895d891
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445445"
---
# <a name="implementing-command-handling-for-nested-projects"></a>实现嵌套项目的命令处理
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IDE 可将通过传递的命令传递<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>和<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口连接到嵌套的项目或父项目可以筛选或重写命令。  
  
> [!NOTE]
> 只有通常由父项目的命令可以进行筛选。 命令，如**构建**并**部署**由处理不能筛选的 IDE。  
  
 以下步骤介绍了如何实现命令处理。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-implement-command-handling"></a>若要实现命令处理  
  
1. 当用户选择嵌套的项目或节点中嵌套项目：  
  
   1. IDE 调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法。  
  
      — 或 —  
  
   2. 如果该命令在层次结构窗口中，如在解决方案资源管理器中的快捷方式菜单命令源自 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>上项目的父方法。  
  
2. 父项目可以检查参数传递给`QueryStatus`，如`pguidCmdGroup`和`prgCmds`，以确定父项目是否应筛选命令。 如果父项目实现来筛选命令，它应设置：  
  
   ```  
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;  
   // make sure it is disabled  
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;  
   ```  
  
    然后父项目应返回`S_OK`。  
  
    如果父项目不会筛选该命令，它应只返回`S_OK`。 在这种情况下，IDE 会自动将命令路由到子项目。  
  
    父项目不需要将命令传送到子项目。 IDE 执行此任务...  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>   
 [命令、 菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)   
 [嵌套项目](../../extensibility/internals/nesting-projects.md)
