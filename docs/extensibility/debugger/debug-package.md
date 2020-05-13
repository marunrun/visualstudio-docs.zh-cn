---
title: 调试包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de6240ea5d938d02f8415009203962e124ff049e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739023"
---
# <a name="debug-package"></a>调试包
调试包在 Visual Studio 外壳中运行，并处理所有 UI。 它使用 Visual Studio 调试接口并与会话调试管理器 （SDM） 通信。

 通过 SDM 发送的中断事件将调试器从运行模式切换到中断模式，并将焦点更改为发生中断的程序。 调试包跟踪堆栈帧和线程从事件发送给它的信息。

 调试包没有语言或运行时环境依赖关系。 不需要实现或修改调试包。

 调试包由*vsdebug.dll*实现。

## <a name="see-also"></a>请参阅
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
- [堆叠帧](../../extensibility/debugger/stack-frames.md)
- [线程](../../extensibility/debugger/threads.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)
