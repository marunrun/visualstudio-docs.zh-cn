---
title: PF | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: cdc0a094-a986-4629-bd1c-dd5fdca323dc
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 243d5fada7342bc05d8768a7e33cca6f55e309ef
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442467"
---
# <a name="pf"></a>PF
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **PF** 选项将采样的分析事件设置为页面错误，还可以选择将采样间隔内的页面错误数从默认值 10 改为其他值。  
  
> [!NOTE]
> PF 不能用于 64 位系统。  
  
 **注意：** 64 位计算机上不支持 PF。只能在包含 **Launch** 或 **Attach** 选项的命令行中使用 **PF**。  
  
 默认情况下，采样事件设置为非暂停处理器时钟周期，采样间隔设置为 10,000,000。 使用 **Timer**、**PF**、**Sys** 和 **Counter** 选项可以设置采样事件和采样间隔。 **GC** 选项在每次发生分配和垃圾回收事件时收集 .NET 内存数据。 在命令行中只能指定这些选项中的一个。  
  
 只能在包含 **Launch** 或 **Attach** 选项的第一个命令行中设置采样事件和采样间隔。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe {/Launch:AppName|/Attach:PID} /PF[:Events] [Options]  
```  
  
#### <a name="parameters"></a>参数  
 `Events`  
 一个整数值，指定采样间隔内页面错误事件的数量。 如果未指定 `Events`，则将间隔设置为 10。  
  
## <a name="required-options"></a>必需选项  
 只能在包含以下选项之一的命令行中指定 **PF**。  
  
 **Launch：** `AppName`  
 启动探查器以及由 AppName 指定的应用程序。  
  
 **Attach:** `PID`  
 将探查器附加到由 AppName 指定的进程。  
  
## <a name="invalid-options"></a>无效选项  
 不能在 **PF** 所在的命令行中指定以下选项。  
  
 **Timer**[ **:** `Cycles`]  
 将采样事件设置为处理器时钟周期，还可以选择将采样间隔设置为 `Cycles`。 默认 Timer 间隔为 10,000,000。  
  
 **Sys**[ **:** `Events`]  
 将采样事件设置为被分析的应用程序对操作系统内核的调用 (syscall)，还可以选择将采样间隔设置为 `Events`。 默认 Sys 间隔为 10。  
  
 **Counter:** `Name`[`,Reload`[`,FriendlyName`]]  
 将采样事件设置为 `Name` 指定的 CPU 性能计数器，并将采样间隔设置为 `Reload`。  
  
 **GC**[ **:** {**Allocation**&#124;**Lifetime**}]  
 收集 .NET 内存数据。 默认情况 (Allocation) 下，每次发生内存分配事件时都收集数据  。 如果指定 Lifetime 参数，则每次发生垃圾回收事件时也收集数据  。  
  
## <a name="example"></a>示例  
 本示例演示如何将分析样本事件设置为页面错误，以及如何将采样间隔设置为 20 个页面错误。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /PF:20  
```  
  
## <a name="see-also"></a>请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
