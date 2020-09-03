---
title: Visual Studio SDK)  (服务器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 32fdbb5afca40c3b4fced468d2f9ef0ea5226c00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712897"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试程序体系结构中， *服务器*：

- 是端口和端口供应商的容器，可将端口和端口供应商传达给会话调试管理器 (SDM) 和调试引擎。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) 接口表示，此接口仅由 visual studio 为运行) 的每个 visual studio 实例 (服务器的一个实例实现。

## <a name="see-also"></a>另请参阅
- [端口](../../extensibility/debugger/ports.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
