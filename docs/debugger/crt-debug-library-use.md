---
title: CRT 调试库的使用 | Microsoft Docs
ms.date: 11/04/2016
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
ms.openlocfilehash: 9434be46f357a97ad01f10ceec184ebe6c52eb43
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62565542"
---
# <a name="crt-debug-library-use"></a>CRT 调试库使用
C 运行时库提供了广泛的调试支持。 若要使用其中一个 CRT 调试库，则必须与 [/DEBUG](/cpp/build/reference/debug-generate-debug-info) 链接，并使用 /MDd、/MTd 或 /LDd 进行编译

## <a name="remarks"></a>备注
 CRT 调试的主要定义和宏可在 CRTDBG.h 头文件中找到。

 CRT 调试库中的函数在编译时带有调试信息([/Z7、 /Zd、 /Zi、 /ZI（调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)），且未经过优化。 一些函数包含断言以验证传递给它们的参数，并提供源代码。 使用此源代码，可以单步执行 CRT 函数以确认函数是否按预期方式工作，并检查是否存在错误的参数或内存状态。 （有些 CRT 技术是专有技术，不提供异常处理、浮点和其他一些例程的源代码。）

 安装 Visual C++ 时，可以选择在硬盘上安装 C 运行库源代码。 如果不安装源代码，将需要 CD-ROM 才能单步执行 CRT 函数。

 有关可以使用的各种运行时库的详细信息，请参阅 [C 运行时库](/cpp/c-runtime-library/crt-library-features)。

## <a name="see-also"></a>请参阅

- [CRT 调试方法](../debugger/crt-debugging-techniques.md)
- [/MD、/MT、/LD（使用运行时库）](/cpp/build/reference/md-mt-ld-use-run-time-library)