---
title: Visual Studio 探查器 API 参考（本机）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- performance tools, API
- Profiler, API
ms.assetid: a0c3be92-c263-4678-9fb9-bafead3bd5f5
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b296ae403658f4d39558c28e11a425adee7650a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431118"
---
# <a name="visual-studio-profiler-api-reference-native"></a>Visual Studio 探查器 API 参考（本机）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 探查器 API 允许你以编程方式控制收集的数据量，并在分析期间插入时间戳和分析标记。 若要使用本机 API，请包含 VSPerf.h 头文件，并在项目中添加 VSPerf.lib。  
  
> [!NOTE]
> 默认情况下，VSPerf.h 和 VSPerf.lib 位于\<驱动器>：\Program Files\Microsoft Visual Studio 9\Team Tools\Performance Tools\PerfSDK 目录中。  
  
## <a name="in-this-section"></a>本节内容  
 [CommentMarkAtProfile](../profiling/commentmarkatprofile.md)  
  
 [CommentMarkProfile](../profiling/commentmarkprofile.md)  
  
 [MarkProfile](../profiling/markprofile.md)  
  
 [NameProfile](../profiling/nameprofile.md)  
  
 [ResumeProfile](../profiling/resumeprofile.md)  
  
 [StartProfile](../profiling/startprofile.md)  
  
 [StopProfile](../profiling/stopprofile.md)  
  
 [SuspendProfile](../profiling/suspendprofile.md)  
  
 [PROFILE_CURRENTID](../profiling/profile-currentid.md)  
  
## <a name="see-also"></a>请参阅  
 [分析工具 API](../profiling/profiling-tools-apis.md)   
 [演练：使用探查器 API](../profiling/walkthrough-using-profiler-apis.md)
