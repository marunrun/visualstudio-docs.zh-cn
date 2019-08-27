---
title: 错误：无法自动单步执行服务器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.causality_no_server_response
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, notification error
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e9d84f4c7f7f58ae980a266b436207c843926ae1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62850143"
---
# <a name="error-unable-to-automatically-step-into-the-server"></a>错误：无法自动单步执行服务器
此错误显示如下：

 无法自动单步执行服务器。 在远程过程执行前调试器未得到通知

 当你尝试单步执行 Web 服务时，可能发生此错误（请参阅 [单步执行 XML Web services](https://msdn.microsoft.com/library/8e67de38-bf5f-41cc-a457-1b88ce63d764)）。 只要 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 未正确设置，就会发生此错误。

 可能的原因有：

- [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序的 web.config 文件未将调试设置为“true”（请参见 [ASP.NET 应用程序中的调试模式](../debugger/how-to-enable-debugging-for-aspnet-applications.md)）。

- 在安装 Visual Studio 后安装了某个版本的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应在安装 Visual Studio 之前安装。 若要修复此问题，请使用“Window 控制面板”>“程序和功能”来修复 Visual Studio 安装。

## <a name="see-also"></a>请参阅
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [远程调试](../debugger/remote-debugging.md)