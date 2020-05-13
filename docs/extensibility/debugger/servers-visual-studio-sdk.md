---
title: 服务器（可视化工作室 SDK） |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712897"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试器体系结构中，*服务器*：

- 是端口和端口供应商的容器，将端口和端口供应商与会话调试管理器 （SDM） 和调试引擎进行通信。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由[IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)接口表示，该接口仅由 Visual Studio 实现（运行的 Visual Studio 的每个实例的服务器的一个实例）。

## <a name="see-also"></a>请参阅
- [港口](../../extensibility/debugger/ports.md)
- [港口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
