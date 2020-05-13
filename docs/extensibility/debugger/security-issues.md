---
title: 安全问题 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40898f5633eac374206ed40bfcac96d9c1c5b753
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713055"
---
# <a name="security-issues"></a>安全问题
要使用 Visual Studio 调试程序，所需的唯一权限与开发人员运行程序所需的权限相同。 这包括大多数情况下的远程调试。 某些涉及其他服务（如 Internet 信息服务）的情况可能需要更高级别的权限。

 当 Visual Studio 运行时，进程调试管理器 （PDM） 跟踪本地计算机上的调试过程。 开发人员远程启动名为*msvsmon.exe*的程序，以处理远程调试并使 PDM 可用。 *（msvsmon.exe*不是服务，必须手动启动才能在该计算机上启用远程调试。当 Visual Studio （或*msvsmon.exe*） 未运行时，不会跟踪任何进程以进行调试。

 开发人员可以调试他们启动的程序，无需特殊权限。 如果其他人是同一安全组的成员，开发人员甚至可以调试由其他人启动的进程。 而且，为了启用远程调试，只需将所需的文件复制到远程计算机并启动*msvsmon.exe。* 有关详细信息，请参阅[远程调试](../../debugger/remote-debugging.md)。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [过程调试管理器](../../extensibility/debugger/process-debug-manager.md)
- [远程调试](../../debugger/remote-debugging.md)
