---
title: 控制台 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: e825ba66-1383-46ad-8712-396bc9c14036
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e947fb28c92323f0d4d66c697c272699fc63450e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161313"
---
# <a name="console"></a>控制台
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe“Console”选项在新的命令提示符窗口中启动指定的应用程序。 “Console”只能与 VSPerfCmd“Launch”选项一起使用。 如果应用程序不是命令行应用程序，“Console”不起作用。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Launch:AppName /Console  
```  
  
#### <a name="parameters"></a>参数  
 None  
  
## <a name="required-options"></a>必需选项  
 只能在同时包含“Launch”选项的命令行上指定“Console”。  
  
 **启动：**`AppName`  
 启动探查器以及由 `AppName` 指定的应用程序。  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
