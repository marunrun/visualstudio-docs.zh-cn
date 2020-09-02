---
title: 报表挂钩函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- FSharp
- VB
- CSharp
- C++
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
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0a492a1db8b65cad74d02cec0f43bf0c81461730
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687511"
---
# <a name="report-hook-functions"></a>报表挂钩函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

每次 [_CrtDbgReport](https://msdn.microsoft.com/library/1ae7c64f-8c84-4797-9574-b59f00f7a509) 生成调试报告时都会调用报告挂钩函数（使用 [_CrtSetReportHook](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc) 安装）。 可以使用报告挂钩函数以及其他项筛选报告以集中于特定类型的分配。 报告挂钩函数应具有如下原型：  
  
```  
int YourReportHook(int nRptType, char *szMsg, int *retVal);  
```  
  
 传递给 _CrtSetReportHook 的指针为 _CRT_REPORT_HOOK 类型，如 CRTDBG.H 中所定义：  
  
```  
typedef int (__cdecl *_CRT_REPORT_HOOK)(int, char *, int *);  
```  
  
 当运行库调用挂钩函数时，nRptType参数包含报告类别（_CRT_WARN、_CRT_ERROR 或 _CRT_ASSERT），szMsg 包含指向完全汇编的报告消息字符串的指针，而 retVal 指定 `_CrtDbgReport` 应在生成报告以后继续正常执行还是启动调试器   。 （retVal 值为零继续执行，值为 1 为启动调试器。）  
  
 如果挂钩完全处理了所讨论的消息，因而不需要进一步的报告，那么应返回 TRUE。 如果返回 FALSE，`_CrtDbgReport` 将以正常方式报告消息。  
  
## <a name="see-also"></a>另请参阅  
 [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 示例](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
