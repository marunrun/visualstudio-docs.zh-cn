---
title: SCRIPT_DEBUGGER_OPTIONS 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SCRIPT_DEBUGGER_OPTIONS Enumeration
ms.assetid: aef41ec0-6f65-48e8-a69e-44b4e4fb929f
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c69d419732786442cda275bf85c74ab2b9d3e870
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574564"
---
# <a name="script_debugger_options-enumeration"></a>SCRIPT_DEBUGGER_OPTIONS 枚举
指示一组适用于附加调试器的选项和/或功能。 在[IDebugApplicationNode100：： GetExcludedDocuments](../../winscript/reference/idebugapplicationnode100-getexcludeddocuments.md)和[IDebugApplicationNode100：： SetFilterForEventSink](../../winscript/reference/idebugapplicationnode100-setfilterforeventsink.md)中使用  
  
> [!IMPORTANT]
> 这些常量由 PDM 10.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef SCRIPT_DEBUGGER_OPTIONS  
```  
  
## <a name="members"></a>Members  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|SDO_NONE|0x00000000|未设置任何选项。|  
|SDO_ENABLE_FIRST_CHANCE_EXCEPTIONS|0x00000001|指示当引发异常时，脚本运行时应引发 BREAKREASON_ERROR 事件。 此选项可以由调试器设置，也可以通过 `Debug.enableFirstChanceExceptions(<true&#124;false>)` 的用户代码进行设置。|  
|SDO_ENABLE_WEB_WORKER_SUPPORT|0x00000002|指示附加调试器支持 web 工作进程。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)