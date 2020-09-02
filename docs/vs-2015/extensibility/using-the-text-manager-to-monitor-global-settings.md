---
title: 使用文本管理器监视全局设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ece51450b8344ae4715a912399ec538171a26a5c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695458"
---
# <a name="using-the-text-manager-to-monitor-global-settings"></a>使用文本管理器监视全局设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果实现核心编辑器，则必须监视全局设置中所做的更改，因为这些更改可能会影响编辑器的实例。 可以通过侦听文本管理器引发的事件来跟踪更改。 例如，当你在核心编辑器中为组件的外观或行为指定全局首选项（如其文档数据对象）时，文本管理器将存储此信息并将其传递给所有受影响的客户端。  
  
## <a name="text-manager-functions"></a>文本管理器函数  
 文本管理器引发了许多设置的事件，其中包括：  
  
- 缓冲区是否受源代码管理  
  
- 如何注册文件更改通知  
  
- 如何跟踪与特定缓冲区关联的视图  
  
- 文本着色首选项  
  
- 制表符与空格首选项  
  
  对于给定语言唯一的首选项不由文本管理器进行管理。 这些设置必须由每个语言服务管理。  
  
  文本管理器的事件通知由 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents> 接口提供。 在客户端对象上实现此接口，以处理引发文本管理器的事件。 使用 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 文本管理器上的接口注册这些事件。  
  
## <a name="see-also"></a>另请参阅  
 [在核心编辑器内](../extensibility/inside-the-core-editor.md)   
 [编辑器功能](https://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)
