---
title: 参数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 20c35949-1f29-4282-ac75-4e6c237d71bc
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65759da4363891c713f906e6cb10f00443bcbceb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197915"
---
# <a name="args"></a>参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **参数**选项指定传递给 **Launch** 子命令的目标应用程序的参数列表。  
  
 只有在命令行上还指定了 **Launch** 时才可使用**参数**。 指定 **Launch** 时，**参数**为可选。  
  
## <a name="syntax"></a>语法  
  
```  
VSPerfCmd.exe /Launch:AppName /Args:Arguments [Options]  
```  
  
#### <a name="parameters"></a>参数  
 `Arguments`  
 **Launch** 命令的目标应用程序的参数列表。  
  
## <a name="required-options"></a>必需选项  
 **Launch：** `AppName`  
 启动指定的应用程序并开始使用采样方法进行分析。  
  
## <a name="example"></a>示例  
 以下示例使用**参数**选项将参数传递给 TestApp.exe。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Args:"123, 'Hello World'"  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
