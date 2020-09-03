---
title: 选择调试引擎实现策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6b03e69892da217d84d56b39b7df61784907d2b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183459"
---
# <a name="choosing-a-debug-engine-implementation-strategy"></a>选择调试引擎实施策略
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用运行时体系结构确定调试引擎 (DE) 实现策略。 调试引擎可能会在进程内创建到要调试的程序，进程内到 Visual Studio 会话调试管理器 (SDM) 或进程外执行。 以下准则可帮助您选择这三种策略。  
  
## <a name="guidelines"></a>指南  
 尽管在 SDM 和要调试的程序中都可以不执行任何操作，但通常没有理由这样做。 跨进程边界的调用相对较慢。  
  
 已为 Win32 本机运行时环境和公共语言运行时环境提供调试引擎。 如果必须将这两种环境中的任何一种都替换为替代，则必须创建与 SDM 的进程内操作。  
  
 否则，你可以选择是为要调试的程序在 SDM 中创建进程内或进程内的进程。 需要考虑的表达式计算器是否需要频繁访问程序符号存储区，以及是否可以将符号存储区加载到内存中以实现快速访问。 也请考虑以下要求：  
  
- 如果表达式计算器和符号存储区之间没有多个调用，或如果符号存储区可以读入 SDM 内存空间，则创建对 SDM 的进程中。 当将调试引擎附加到程序时，必须将其 CLSID 返回到 SDM。 SDM 使用此 CLSID 创建 DE 的进程内实例。  
  
- 如果 DE 必须调用程序才能访问符号存储区，请使用该程序创建进程内操作。 在这种情况下，程序将创建 DE 的实例。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
