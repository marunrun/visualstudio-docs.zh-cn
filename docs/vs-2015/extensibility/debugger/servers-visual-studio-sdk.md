---
title: Visual Studio SDK)  (服务器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ed2ce924b22827a82a67664e3e473f0930a87e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199407"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **服务器**：  
  
- 是端口和端口供应商的容器，用于将端口和端口供应商传达给会话调试管理器 (SDM) 和调试引擎。  
  
- 可以按名称标识自身，并枚举其端口和端口供应商。  
  
- 由 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) 接口表示，此接口仅由 visual studio 为运行) 的每个 visual studio 实例 (服务器的一个实例实现。  
  
## <a name="see-also"></a>另请参阅  
 [端口](../../extensibility/debugger/ports.md)   
 [端口供应商](../../extensibility/debugger/port-suppliers.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
