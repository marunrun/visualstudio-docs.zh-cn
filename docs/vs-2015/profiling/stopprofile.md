---
title: StopProfile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- StopProfile
ms.assetid: be75b03c-7af5-4abe-a54a-6ee5479ad877
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b8be45de29f379161845cc7ba8ec58d2d1bc9285
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193301"
---
# <a name="stopprofile"></a>StopProfile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`StopProfile` 函数将指定分析级别的计数器设置为 0（关闭）。  
  
## <a name="syntax"></a>语法  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI StopProfile(  
                       PROFILE_CONTROL_LEVEL Level,   
                       unsigned int dwId);  
```  
  
#### <a name="parameters"></a>参数  
 `Level`  
  
 指示性能数据集合可应用到的分析级别。 以下 PROFILE_CONTROL_LEVEL 枚举器可用于指示性能数据集合可应用到的三个级别之一  ：  
  
|枚举器|说明|  
|----------------|-----------------|  
|PROFILE_GLOBALLEVEL|全局级别设置影响分析运行中的所有进程和线程。|  
|PROFILE_PROCESSLEVEL|进程级别设置影响指定进程包含的所有线程。|  
|PROFILE_THREADLEVEL|线程分析级别设置影响指定的线程。|  
  
 `dwId`  
  
 系统生成的进程或线程标识符。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 函数通过使用 **PROFILE_COMMAND_STATUS** 枚举来指示成功或失败。 返回值可以是下列值之一：  
  
|枚举器|说明|  
|----------------|-----------------|  
|PROFILE_ERROR_ID_NOEXIST|分析元素 ID 不存在。|  
|PROFILE_ERROR_LEVEL_NOEXIST|指定的分析级别不存在。|  
|PROFILE_ERROR_MODE_NEVER|调用函数时，分析模式设置为“从不”。|  
|PROFILE_ERROR_NOT_YET_IMPLEMENTED|分析函数调用、分析级别或者调用和级别的组合尚未实现。|  
|PROFILE_OK|调用成功。|  
  
## <a name="remarks"></a>备注  
 StartProfile 和 StopProfile 控制分析级别的启动/停止状态。 启动/停止的默认值为 1。 可在注册表中更改初始值。 每次调用 StartProfile 会将启动/停止设置为 1；每次调用 StopProfile 会将其设置为 0。  
  
 当启动/停止大于 0 时，该级别的启动/停止状态为 ON。 当它小于或等于 0 时，启动/停止状态为 OFF。  
  
 当启动/停止状态和挂起/继续状态都为 ON 时，该级别的分析状态为 ON。 对于要分析的线程，该线程的全局、进程和线程级别状态都必须为 ON。  
  
## <a name="net-framework-equivalent"></a>.NET Framework 等效项  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>函数信息  
 标头：在 VSPerf.h 中声明  
  
 导入库：VSPerf.lib  
  
## <a name="example"></a>示例  
 下面的示例演示 StopProfile 方法。 该示例假定已对由 [PROFILE_CURRENTID](../profiling/profile-currentid.md) 标识的同一线程或进程调用了 StartProfile 方法。  
  
```  
void ExerciseStopProfile()  
{  
    // StartProfile and StopProfile control the   
    // Start/Stop state for the profiling level.   
    // The default initial value of Start/Stop is 1.   
    // The initial value can be changed in the registry.   
    // Each call to StartProfile sets Start/Stop to 1;   
    // each call to StopProfile sets it to 0.   
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare enumeration to hold result of call  
    // to StopProfile.  
    PROFILE_COMMAND_STATUS profileResult;  
  
    profileResult = StopProfile(  
        PROFILE_THREADLEVEL,  
        PROFILE_CURRENTID);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("StopProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, profileResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 探查器 API 参考 (本机) ](../profiling/visual-studio-profiler-api-reference-native.md)
