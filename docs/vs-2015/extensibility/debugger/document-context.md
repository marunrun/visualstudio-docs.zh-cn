---
title: 文档上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3034c9ca02fca8e91eb1aa5e4d0eb5a2fe1f773f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200587"
---
# <a name="document-context"></a>文档上下文
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试中， **文档上下文**：  
  
- 表示源文件中的位置。 对于源文件可能不存在的语言，文档上下文标识通常由运行时环境生成的文档中的位置。 例如，脚本引擎可能通过脚本生成文档。 有关详细信息，请参阅 [文档位置](../../extensibility/debugger/document-position.md)。  
  
- 描述与代码上下文对应的源文档中的位置。 符号处理程序使用由编译器或解释器生成的信息将代码上下文映射到文档上下文。  
  
- 由 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口实现。  
  
## <a name="see-also"></a>另请参阅  
 [代码上下文](../../extensibility/debugger/code-context.md)   
 [符号提供程序](../../extensibility/debugger/symbol-provider.md)   
 [符号提供程序接口](../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
