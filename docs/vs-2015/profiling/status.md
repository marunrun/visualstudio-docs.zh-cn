---
title: Status | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ba656fa4-ef9d-4d8c-a3b6-739c3b5d23ae
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f64364caf914c030fef806c5ae17e90a8368fa3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157791"
---
# <a name="status"></a>状态
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **Status** 选项显示有关探查器状态以及当前正在分析的任何进程的信息。  
  
 **Status** 选项必须是命令行中指定的唯一选项。 必须先使用 VSPerfCmd.exe **Start** 选项初始化探查器，然后才能显示任何状态。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Status  
```  
  
#### <a name="parameters"></a>参数  
 无  
  
## <a name="remarks"></a>备注  
 **Status** 选项显示探查器的以下状态信息。  
  
 **输出文件名**  
 当前探查器数据文件的路径和文件名。  
  
 **收集模式**  
 采样或跟踪  
  
 **最大进程数**  
 一次可分析的最大进程数和当前活动的进程数。  
  
 **最大线程数**  
 一次可分析的最大线程数。  
  
 **缓冲区数**  
 专用于写入分析数据的内存缓冲区数。  
  
 **缓冲区的大小**  
 内存缓冲区的大小（以字节为单位）。  
  
 **Status** 选项显示当前正在分析的每个进程的以下状态信息。  
  
 **Process**  
 被分析进程的名称。  
  
 **进程 ID**  
 进程的系统标识符。  
  
 **线程数**  
 当前正在执行的线程数。  
  
 **启动/停止计数**  
 用于控制此进程的数据收集的主要内部探查器计数。 该计数必须等于一才能收集数据。 启动/停止计数可以通过探查器 API 以及 VSPerfCmd 选项 **GlobalOn**、**GlobalOff**、**ProcessOn**、**ProcessOff**、**ThreadOn** 和 **ThreadOff** 进行控制。  
  
 **挂起/继续计数**  
 用于控制此进程的数据收集的辅助内部探查器计数。 该计数必须小于或等于零才能收集数据。 “挂起/继续”  计数只能通过探查器 API 进行控制。  
  
 **有监视器访问权限的用户**  
 列出有权访问探查器的用户名。 可以使用 VSPerfCmd.exe **Admin** 选项向其他用户授予访问权  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
