---
title: 调试器不能显示源代码或反汇编
description: 查看消息“代码在当前位置停止执行，但调试器不能显示当前位置的源代码或反汇编”的原因。
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- disassembly code, errors
ms.assetid: 112d3ea3-fdd2-4bce-92b4-167a76258934
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dd0ed9a798c29010911a1537c99f30ba44e01aea
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96561040"
---
# <a name="debugger-cannot-display-source-code-or-disassembly"></a>调试器不能显示源代码或反汇编
此错误显示如下：

 代码在当前位置停止执行，但调试器不能显示当前位置的源代码或反汇编。

 该错误信息可能由于许多原因而发生：

- 可能在调试不支持汇编的语言时在无源代码的位置命中了某个断点。 打开“断点”窗口，确定断点的位置，然后删除该断点。

- 如果正在调试脚本，则可能在程序中无线程时命中了某个断点。 从“调试”菜单中选择“单步执行”或“继续”以继续进行调试  。

- 出于安全考虑，可能禁止调试器从在调试的程序中读取堆栈、线程和其他上下文信息。 如果正在调试 Web 应用程序，且没有访问虚拟内存的正确权限，则这种情况最可能发生。 将虚拟目录的安全设置为 Anonymous 并再次尝试。

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)