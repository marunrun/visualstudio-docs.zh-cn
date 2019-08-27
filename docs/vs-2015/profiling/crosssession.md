---
title: CrossSession | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: b9fcb9c3-7903-478c-9b7c-dbd94092fcba
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 05e1f2360b3257e44fde1af8be3554dd7fd95115
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537172"
---
# <a name="crosssession"></a>CrossSession
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe“CrossSession”选项使探查器可以从任何控制台会话收集数据。 “CrossSession”选项必须与“Start”选项一起使用。  
  
 可以使用缩写 CS 代替 CrossSession。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Start:Method /CrossSession [Options]  
```  
  
#### <a name="parameters"></a>参数  
 None  
  
## <a name="valid-options"></a>有效选项  
 若要在另一个会话中启用分析，必须使用“Start”选项指定“CrossSession”选项。 “CrossSession”还必须在任何后续“VSPerfCmd Attach”和“Detach”命令中进行指定。  
  
 **Start:** `Method`  
 “Start”选项可将探查器初始化为指定的分析方法。  
  
 **Attach:** _PID_[**,**_PID_]  
 开始分析指定进程。  
  
 **Detach**[**:**_PID_[,_PID_]]  
 停止分析指定进程。  
  
## <a name="example"></a>示例  
 在此示例中，“CrossSession”选项用于附加到在另一个控制台会话中启动的应用程序。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /CrossSession  
VSPerfCmd.exe /Attach:12345 /CS  
```  
  
## <a name="see-also"></a>请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
