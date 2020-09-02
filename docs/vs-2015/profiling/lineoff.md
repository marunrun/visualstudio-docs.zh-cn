---
title: LineOff | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 76082063-20ef-47ae-ad64-81b43b654865
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fbe8a715c5bb179c5293dd666f1879c07068d8b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62583166"
---
# <a name="lineoff"></a>LineOff
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，使用采样分析方法时，探查器将收集源代码行号和行号偏移量数据。 使用 VSPerfCmd 启动应用程序时，VSPerfCmd 的“LineOff”  选项会禁止收集行号数据。 指定“LineOff”  后，将在函数级别收集分析数据。  
  
 只能将“LineOff”  与“Launch”  选项一起使用，且只有在使用 Start:Sample   选项将探查器初始化为采样后才能这样使用。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Launch:AppName /LineOff [Options]  
```  
  
#### <a name="parameters"></a>参数  
 None  
  
## <a name="required-options"></a>必需选项  
 只能在包含“Launch”  选项的命令行上使用“LineOff”  选项。  
  
 **启动：**`AppName`  
 启动指定的应用程序并开始使用采样方法进行分析。  
  
## <a name="example"></a>示例  
 此示例启动应用程序和探查器，并禁止行级采样。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /LineOff  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
