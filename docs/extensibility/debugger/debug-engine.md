---
title: 调试引擎 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a4cb00796f8db23a43cd81a06d80d0fac40f075e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739064"
---
# <a name="debug-engine"></a>调试引擎
调试引擎 （DE） 与解释器或操作系统配合使用，以提供调试服务，如执行控制、断点和表达式计算。 DE 负责监视正在调试的程序的状态。 为此，DE 使用受支持的运行时可用的任何方法，无论是从 CPU 还是从运行时提供的 API。

 例如，通用语言运行时 （CLR） 提供机制，通过 ICorDebugXXX 接口监视正在运行的程序。 支持 CLR 的 DE 使用适当的 ICorDebugXXX 接口来跟踪正在调试的托管代码程序。 然后，它将状态的任何更改传达给会话调试管理器 （SDM），该管理器将此类信息转发给[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

> [!NOTE]
> 调试引擎以特定运行时为目标，即运行正在调试的程序的系统。 CLR 是托管代码的运行时，Win32 运行时适用于本机 Windows 应用程序。 如果创建的语言可以针对这两个运行时之一，则[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]已提供必要的调试引擎。 所有要实现的只是表达式赋值器。

## <a name="debug-engine-operation"></a>调试引擎操作
 监视服务通过 DE 接口实现，并可能导致调试包在不同的操作模式之间转换。 有关详细信息，请参阅[操作模式](../../extensibility/debugger/operational-modes.md)。 每个运行时环境通常只有一个 DE 实现。

> [!NOTE]
> 虽然对 Transact-SQL 和[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]（VBScript） 有单独的[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]DE 实现，并且共享单个 DE。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试使调试引擎能够运行以下两种方式之一：要么与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell 在同一进程中，要么与正在调试的目标程序在同一进程中运行。 当正在调试的进程实际上是在解释器下运行的脚本时，通常会出现后一种形式。 调试引擎必须对解释器有深入的了解才能监视脚本。 在这种情况下，解释器实际上是一个运行时;调试引擎适用于特定的运行时实现。 此外，单个 DE 的实现可以跨进程和计算机边界（例如远程调试）拆分。

 DE 公开[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试接口。 所有通信均通过 COM。 无论 DE 是在进程内、进程外加载还是在另一台计算机上加载，都不会影响组件通信。

 DE 与表达式赋值器组件配合使用，使该特定运行时的 DE 能够理解表达式的语法。 DE 还与符号处理程序组件一起访问语言编译器生成的符号调试信息。 有关详细信息，请参阅[表达式赋值器](../../extensibility/debugger/expression-evaluator.md)和[符号提供程序](../../extensibility/debugger/symbol-provider.md)。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
