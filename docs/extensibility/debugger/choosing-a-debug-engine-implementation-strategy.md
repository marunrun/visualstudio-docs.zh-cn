---
title: 选择调试引擎实现策略 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739125"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>选择调试引擎实现策略
使用运行时体系结构确定调试引擎 (DE) 实现策略。 可以在正在进行调试的程序的进程内创建调试引擎。 在 Visual Studio 会话调试管理器 (SDM) 中创建调试引擎。 或者，为这两个进程创建调试引擎。 以下准则可帮助您选择这三种策略。

## <a name="guidelines"></a>指南
 虽然在 SDM 和正在调试的程序中都可以不执行任何操作，但通常没有理由这样做。 跨进程边界的调用相对较慢。

 已为 Win32 本机运行时环境和公共语言运行时环境提供调试引擎。 如果需要替换任一环境的 DE，应使用 SDM 创建进程内操作。

 否则，您可以为要调试的程序创建 SDM 或进程内的进程内操作。 如果 DE 的表达式计算器需要频繁访问程序符号存储区，则需要考虑。 或者，如果可以将符号存储区加载到内存中，以便快速访问。 另外，请考虑以下方法：

- 如果表达式计算器和符号存储区之间没有多个调用，或如果符号存储区可以读入 SDM 内存空间，则创建对 SDM 的进程中。 当将调试引擎附加到程序时，必须将其 CLSID 返回到 SDM。 SDM 使用此 CLSID 创建 DE 的进程内实例。

- 如果 DE 必须调用程序才能访问符号存储区，请使用该程序创建进程内操作。 在这种情况下，程序将创建 DE 的实例。

## <a name="see-also"></a>另请参阅
- [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
