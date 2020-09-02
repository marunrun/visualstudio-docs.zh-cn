---
title: Timer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1971868e-89fa-4452-8ee7-76e4daf31b66
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1e5f6c6db903b3ecced2ac3ebc4aaa0a3e60910c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145504"
---
# <a name="timer"></a>计时器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **Timer** 选项将采样的分析事件设置为处理器时钟周期，还可以选择将采样间隔内的周期数从默认值 10,000,000 改为其他值。 在 1GH（1 千兆赫）的处理器上，10,000,000 个时钟周期大约为每秒 100 个样本。 可指定的最小周期数为 50,000。  
  
 只有在使用采样分析方法时才能使用 **Timer**，并且只能在包含 **Launch** 或 **Attach** 选项的命令行中使用它。  
  
 默认情况下，将探查器采样事件设置为处理器时钟周期，并将采样间隔设置为 10,000,000。 使用 **Timer**、**PF**、**Sys** 和 **Counter** 选项可以设置采样事件和采样间隔。 **GC** 选项在每次发生分配和垃圾回收事件时收集 .NET 内存数据。 在命令行中只能指定这些选项中的一个。  
  
 只能在包含 **Launch** 或 **Attach** 选项的第一个命令行中设置采样事件和采样间隔。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe {/Launch:AppName|/Attach:PID} /Timer[:Cycles] [Options]  
```  
  
#### <a name="parameters"></a>参数  
 `Cycles`  
 指定采样间隔中处理器时钟周期数的一个整数值。 如果未指定 `Cycles`，则将间隔设置为 10,000,000。 指定值时不要含有逗号。  
  
## <a name="required-options"></a>必需选项  
 只能在包含以下选项之一的命令行中指定 **Timer**。  
  
 **启动：**`AppName`  
 启动探查器以及由 `AppName` 指定的应用程序。  
  
 **附加：**`PID`  
 将探查器附加到进程 ID (`PID`) 指定的进程。  
  
## <a name="invalid-options"></a>无效选项  
 不能在 **Timer** 所在的命令行中指定以下选项。  
  
 **PF**[**：** `Events` ]  
 将采样事件设置为页面错误，根据需要还可以将采样间隔设置为 `Events`。 默认 PF 间隔为 10。  
  
 **Sys**[**：** `Events` ]  
 将采样事件设置为操作系统调用，根据需要还可以将采样间隔设置为 `Events`。 默认 Sys 间隔为 10。  
  
 **计数器**[**：** `Name,Reload,FriendlyName` ]  
 将采样事件设置为 `Name` 指定的 CPU 性能计数器，并将采样间隔设置为 `Reload`。  
  
 **GC**[**:**{**Allocation**&#124;**Lifetime**}]  
 收集 .NET 内存数据。 默认情况下 (**分配**) ，会在每个内存分配事件时收集数据。 如果指定 Lifetime 参数，则每次发生垃圾回收事件时也收集数据****。  
  
## <a name="example"></a>示例  
 此示例演示如何将探查器采样间隔设置为 1,000,000 个处理器周期。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Timer:1000000  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
