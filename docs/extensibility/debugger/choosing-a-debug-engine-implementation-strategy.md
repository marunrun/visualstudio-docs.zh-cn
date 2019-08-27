---
title: 选择调试引擎实施策略 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 930908b66b5d2234b8c62585b10ddf751c96f61c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324509"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>选择调试引擎实施策略
使用运行时体系结构来确定您的调试引擎 (DE) 实施策略。 可以创建调试引擎中的进程进行调试的程序。 创建调试引擎进程内运行 Visual Studio 会话调试管理器 (SDM)。 或者，创建调试引擎的进程外对这两个值。 以下指导原则可帮助您在以下三个策略之间进行选择。

## <a name="guidelines"></a>准则
 虽然可以为 DE 为进程外 SDM 和正在调试的程序，没有通常无需执行此操作。 跨进程边界的调用是相对较慢。

 调试引擎已提供 Win32 本机运行时环境和公共语言运行时环境。 如果必须替换为这两种环境 DE，应使用 SDM 创建 DE 进程内。

 否则为您可以创建 DE 进程内运行到 SDM 或进程的程序进行调试。 您需要考虑 DE，表达式计算器是否需要频繁访问程序符号存储区。 或者，如果符号存储区可以加载到内存中以便快速访问。 此外，请考虑以下方法：

- 如果不是表达式计算器和符号存储区之间的多个调用或符号存储区可以读取到 SDM 内存空间，创建 DE 进程内运行到 SDM。 它将附加到你的程序时，您必须返回到 SDM 调试引擎的 CLSID。 SDM 使用此 CLSID 来创建 DE 的进程内实例。

- 如果 DE 必须调用程序访问符号存储区，创建包含此程序中进程 DE。 在这种情况下，该程序创建 DE 的实例。

## <a name="see-also"></a>请参阅
- [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)