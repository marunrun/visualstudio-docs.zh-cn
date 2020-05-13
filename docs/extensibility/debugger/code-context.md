---
title: 代码上下文 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739150"
---
# <a name="code-context"></a>代码上下文
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试中，**代码上下文**：

- 提供调试引擎 （DE） 已知的代码中位置的抽象。 对于当今的大多数运行时体系结构，可以将代码上下文视为程序指令流中的地址。 对于代码可能由指令表示的非传统语言，代码上下文可能通过其他某种方式表示。

- 描述正在调试的程序的执行流中的当前位置。

- 仅当程序在断点停止时才存在。

- 具有关联的文档上下文。

- 由[IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md)接口实现。

## <a name="see-also"></a>请参阅
- [文档上下文](../../extensibility/debugger/document-context.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
