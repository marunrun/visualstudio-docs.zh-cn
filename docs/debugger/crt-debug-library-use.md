---
title: CRT 调试库的使用 | Microsoft Docs
description: 了解 C 运行时 (CRT) 库如何支持调试工作，以及使用 CRT 调试库时必须执行的操作。
ms.custom: SEO-VS-2020
ms.date: 10/03/2019
ms.topic: conceptual
f1_keywords:
- c.debug.runtime
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /DEBUG linker option [C++]
- crtdbg.h file
- debug library
- MDd compiler option [C++]
- libraries, CRT debug library
- MTd compiler option [C++]
- LDd compiler function [C++]
- /MTd compiler option [C++]
- /MDd compiler option [C++]
- debugging [CRT], CRT debug library
- DEBUG linker option [C++]
- /LDd compiler function [C++]
ms.assetid: 464de16b-4215-4787-9bfa-921aaff9d9f4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d145ccd8764e488a5d1270985050b29bcd8987d
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560559"
---
# <a name="crt-debug-library-use"></a>CRT 调试库使用
C 运行时库提供了广泛的调试支持。 若要使用其中一个 CRT 调试库，则必须与 [/DEBUG](/cpp/build/reference/debug-generate-debug-info) 链接，并使用 /MDd  、/MTd  或 /LDd  进行编译

## <a name="remarks"></a>备注
 CRT 调试的主要定义和宏可在 CRTDBG.h 头文件中找到。

 CRT 调试库中的函数编译时带有调试信息（[/Z7、/Zd、/Zi、/ZI（调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)），不进行优化。 某些函数包含断言以验证传递给它们的参数，并且提供源代码。 使用此类源代码，可以单步执行 CRT 函数，以确认这些函数按预期方式工作并检查错误的参数或内存状态。 （某些 CRT 技术是专有技术，不提供用于异常处理、浮点和少数其他例程的源代码。）

 有关可以使用的各种运行时库的详细信息，请参阅 [C 运行时库](/cpp/c-runtime-library/crt-library-features)。

## <a name="see-also"></a>请参阅

- [CRT 调试方法](../debugger/crt-debugging-techniques.md)
- [/MD、/MT、/LD（使用运行时库）](/cpp/build/reference/md-mt-ld-use-run-time-library)