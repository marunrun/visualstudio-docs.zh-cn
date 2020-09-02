---
title: 本机运行时检查自定义 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 434f2425b1eeefd82b954e47a8ced55491a7ec11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697823"
---
# <a name="native-run-time-checks-customization"></a>本机运行时检查自定义
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在使用 /RTC（运行时检查）进行编译或使用 `runtime_checks` 杂注时，C 运行时库会提供本机运行时检查。 某些情况下，可能需要自定义运行时检查：  
  
- 将运行时检查信息传送到默认以外的文件或目标。  
  
- 为第三方调试器的运行时检查信息指定输出目标。  
  
- 报告用 C 运行库发布版本编译的程序中的运行时检查信息。 该库的发布版本不使用 `_CrtDbgReportW` 报告运行时错误。 相反，它们为每个运行时错误显示“断言”对话框。  
  
  若要自定义运行时错误检查，可以：  
  
- 编写一个运行时错误报告函数。 有关详细信息，请参阅[如何：编写运行时错误报告函数](../debugger/how-to-write-a-run-time-error-reporting-function.md)。  
  
- 自定义错误消息目标。  
  
- 查询有关运行时检查错误的信息。  
  
## <a name="customize-the-error-message-destination"></a>自定义错误消息目标  
 如果使用 `_CrtDbgReportW` 报告错误，可以使用 `_CrtSetReportMode` 指定错误消息的目标。  
  
 如果使用自定义报告函数，则使用 `_RTC_SetErrorType` 将错误与报告类型关联。  
  
## <a name="query-for-information-about-run-time-checks"></a>查询有关运行时检查的信息  
 `_RTC_NumErrors` 返回运行时错误检查所检测到的错误类型的数量。 要得到每个错误的简短说明，可以从 0 循环到 `_RTC_NumErrors` 的返回值，并在每次循环中将迭代值传递给 `_RTC_GetErrDesc`。 有关详细信息，请参阅 [_RTC_NumErrors](https://msdn.microsoft.com/library/7e82adae-38e2-4f8b-bc0b-37bda8109fd1) 和 [_RTC_GetErrDesc](https://msdn.microsoft.com/library/7994ec2b-5488-4fd4-806d-a166c9a9f927)。  
  
## <a name="see-also"></a>另请参阅  
 [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)   
 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b)   
 [_CrtDbgReport、_CrtDbgReportW](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc)
