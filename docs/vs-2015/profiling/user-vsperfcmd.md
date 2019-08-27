---
title: User (VSPerfCmd) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ee1a478e-374d-4f30-ae28-d260b9d4723a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 311d02ad3e15f184f8b7e21b5794d73c41a8d4fb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145377"
---
# <a name="user-vsperfcmd"></a>User (VSPerfCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**User** 选项指定拥有被分析进程的帐户的域和用户名。 仅在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。  
  
 **用户**选项只能在还包含命令行上指定**启动**选项选项。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Start:Method /Output:FileName /User:[Domain\]UserName [Options]  
```  
  
#### <a name="parameters"></a>参数  
 `Domain`  
 用户域的名称。  
  
 `UserName`  
 用户的名称。  
  
## <a name="required-options"></a>必需选项  
 **User** 选项只能与 **Start** 选项一起使用。  
  
 **Start:** `Method`  
 将探查器初始化为指定的分析方法。  
  
## <a name="example"></a>示例  
 下面的示例演示 **User** 选项的用法。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /User:SYSTEM  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
