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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184264"
---
# <a name="context-menus"></a>上下文菜单
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当用户在工作区活动区域中右键单击时显示上下文菜单，并在释放鼠标右键时显示。  
  
## <a name="editor-context-menus"></a>编辑器上下文菜单  
 通过拦截 `ECMD_SHOWCONTEXTMENU` ，语言服务可以控制将在编辑器中显示的上下文菜单。 若要显示你自己的上下文菜单，请在通过调用将其传递到来处理此命令 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> 。 如果不处理此命令，则 IDE 将显示为编辑器提供的标准上下文菜单。 还可以基于每个标记来控制上下文菜单的内容。 有关此内容的详细信息，请参阅 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md) 和 [截取旧版语言服务命令](../extensibility/internals/intercepting-legacy-language-service-commands.md)。  
  
## <a name="see-also"></a>另请参阅  
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
