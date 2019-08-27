---
title: 报表挂钩函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- hooks, report
- _CrtDbgReport function
- debugger, report hook functions
- memory allocation, debug heap
- debugging [C++], hook functions
- _CrtSetReportHook function
- report hook functions
ms.assetid: 1854bca7-d7eb-4502-89bf-b1ee64cb50ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6f2723304fe22af9ae2920ff828c953de9347449
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902679"
---
# <a name="report-hook-functions"></a>报表挂钩函数
每次 [_CrtDbgReport](/cpp/c-runtime-library/reference/crtsetreporthook) 生成调试报告时都会调用报告挂钩函数（使用 [_CrtSetReportHook](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw) 安装）。 可以使用报告挂钩函数以及其他项筛选报告以集中于特定类型的分配。 报告挂钩函数应具有如下原型：

```cpp
int YourReportHook(int nRptType, char *szMsg, int *retVal);
```

 将指针传递给 **_CrtSetReportHook**属于类型 **_CRT_REPORT_HOOK**CRTDBG 中定义。H:

```cpp
typedef int (__cdecl *_CRT_REPORT_HOOK)(int, char *, int *);
```

 当运行库调用挂钩函数时，nRptType参数包含报告类别（_CRT_WARN、_CRT_ERROR 或 _CRT_ASSERT），szMsg 包含指向完全汇编的报告消息字符串的指针，而 retVal 指定 `_CrtDbgReport` 应在生成报告以后继续正常执行还是启动调试器。 （retVal 值为零继续执行，值为 1 为启动调试器。）

 如果挂钩完全处理了所讨论的消息，因而不需要进一步的报告，那么应返回 TRUE。 如果返回 FALSE，`_CrtDbgReport` 将以正常方式报告消息。

## <a name="see-also"></a>请参阅
- [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)
- [crt_dbg2 示例](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/crt/crt_dbg2)
