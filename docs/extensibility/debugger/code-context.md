---
title: 代码上下文 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6424c1182f30b1bbfe6c166209b94afb7ec45549
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739150"
---
# <a name="code-context"></a>代码上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中， **代码上下文**：

- 在代码中提供对调试引擎已知的位置的抽象 (DE) 。 对于今天的大多数运行时结构，可以将代码上下文视为程序的指令流中的地址。 对于 nontraditional 语言，其中的代码不能通过说明进行表示，代码上下文可以用其他方式表示。

- 描述正在调试的程序的执行流中的当前位置。

- 仅当程序在断点处停止时才存在。

- 具有关联的文档上下文。

- 由 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) 接口实现。

## <a name="see-also"></a>另请参阅
- [文档上下文](../../extensibility/debugger/document-context.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
