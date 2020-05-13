---
title: 选择调试引擎实施策略 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05e66975a2d41108d3d9fb469da9e4a36a10d8d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739125"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>选择调试引擎实施策略
使用运行时体系结构确定调试引擎 （DE） 实现策略。 您可以将调试引擎创建到正在调试的程序的进程。 在过程中创建调试引擎到可视化工作室会话调试管理器 （SDM）。 或者，将调试引擎创建进程外，以将其与它们进行。 以下指南将帮助您从这三种策略中进行选择。

## <a name="guidelines"></a>指南
 虽然 DE 可能会与 SDM 和正在调试的程序都进行进程外处理，但通常没有理由这样做。 跨进程边界的调用相对较慢。

 已经为 Win32 本机运行时环境和通用语言运行时环境提供了调试引擎。 如果必须为任一环境替换 DE，则应使用 SDM 创建进程中的 DE。

 否则，您将在进程中创建 DE 到 SDM 或进程内到要调试的程序。 您需要考虑 DE 的表达式赋值器是否需要频繁访问程序符号存储。 或者，如果符号存储可以加载到内存中以便快速访问。 此外，请考虑以下方法：

- 如果表达式赋值器和符号存储之间没有多次调用，或者如果符号存储可以读取到 SDM 内存空间中，请创建 SDM 过程中的 DE 进程。 当调试引擎的 CLSID 附加到程序时，必须将其返回到 SDM。 SDM 使用此 CLSID 创建 DE 的进程内实例。

- 如果 DE 必须调用程序才能访问符号存储，请使用程序创建进程中的 DE。 在这种情况下，程序将创建 DE 的实例。

## <a name="see-also"></a>请参阅
- [可视化工作室调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
