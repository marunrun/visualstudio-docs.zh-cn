---
title: 安全问题 |Microsoft Docs
description: 了解使用 Visual Studio 调试程序所需的权限，包括远程调试和涉及其他服务的情况。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 632150101b966e128e8a34636b01a369a1db5c64
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847606"
---
# <a name="security-issues"></a>安全问题
若要使用 Visual Studio 调试程序，只需一个开发人员运行程序所需的权限。 这包括在大多数情况下的远程调试。 某些情况下，涉及其他服务（如 Internet 信息服务）可能需要更高级别的权限。

 当 Visual Studio 正在运行时，进程调试管理器 (PDM) 跟踪本地计算机上的调试进程。 远程，由开发人员启动名为 *msvsmon.exe* 的程序来处理远程调试并使 PDM 可用。  (*msvsmon.exe* 不是服务，必须手动启动才能在该计算机上启用远程调试。 ) 当 Visual Studio (或 *msvsmon.exe*) 未运行时，将不跟踪进程用于调试。

 开发人员可以调试他们启动但没有任何特殊权限的程序。 即使其他人是同一安全组的成员，开发人员甚至可以调试其他人启动的进程。 若要启用远程调试，只需将所需文件复制到远程计算机并开始 *msvsmon.exe*。 有关详细信息，请参阅[远程调试](../../debugger/remote-debugging.md)。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [进程调试管理器](../../extensibility/debugger/process-debug-manager.md)
- [远程调试](../../debugger/remote-debugging.md)
