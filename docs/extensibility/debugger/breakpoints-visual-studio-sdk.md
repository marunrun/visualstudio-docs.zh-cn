---
title: 断点（可视化工作室 SDK） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c9d61c82886f237e8c9f544a59d8fe167548277
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739188"
---
# <a name="breakpoints-visual-studio-sdk"></a>断点 (Visual Studio SDK)
有三种类型的断点：挂起、绑定和错误。

 **挂起的断点：**

- 是一个抽象，它包含将断点绑定到一个或多个程序中的一个或多个代码上下文所需的所有信息。 每次调试程序会导致代码加载时，调试引擎都会检查所有挂起的断点，以查看是否可以绑定它们。

   挂起的断点本身从不绑定到代码，而是收集并据说包含它生成的所有绑定断点。

- 由[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口表示。

  **绑定断点：**

- 是与单个代码上下文关联或绑定到单个代码上下文的断点的抽象。 每个绑定断点都是为了响应挂起的断点而生成的。 但是，挂起的断点可以生成多个绑定断点。

   卸载代码时，可以取消绑定断点并丢弃绑定断点。

- 由[IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)接口表示。

  **错误断点：**

- 是描述尝试将挂起的断点绑定到代码上下文时的错误的抽象。 错误断点描述位置或断点表达式本身的错误。 有关详细信息，请参阅[绑定断点](../../extensibility/debugger/binding-breakpoints.md)。

   断点错误可以是错误或警告。

- 由[IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)接口表示。

## <a name="see-also"></a>请参阅
- [程序](../../extensibility/debugger/programs.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
