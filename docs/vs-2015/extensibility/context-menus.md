---
title: 上下文菜单 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - context menus
ms.assetid: 44fd9e6a-6d42-4aba-80ba-f37fa0070f1d
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9baab8ef64fa1952eff138165f608e25960c8cfd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184264"
---
# <a name="context-menus"></a>上下文菜单
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

上下文菜单时在用户右键单击工作区的活动区域中显示，并清除并释放鼠标右键按钮时。  
  
## <a name="editor-context-menus"></a>编辑器上下文菜单  
 通过截获`ECMD_SHOWCONTEXTMENU`，语言服务可以控制将在编辑器中显示的上下文菜单。 若要显示您自己的上下文菜单，请处理此命令时传递到您<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>。 如果不处理此命令，则 IDE 将显示为编辑器提供一个标准的上下文菜单。 此外可以控制在每个标记的基础上的上下文菜单的内容。 有关详细信息，请参阅[使用旧版 API 使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)并[截获旧版语言服务命令](../extensibility/internals/intercepting-legacy-language-service-commands.md)。  
  
## <a name="see-also"></a>请参阅  
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
