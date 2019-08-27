---
title: SCRIPTGCTYPE 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f289cc7d-2a69-4720-bee0-ea27d054f308
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0a5de3ea949203ad7a6dca0ea777fdbc9514ba6d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840234"
---
# <a name="scriptgctype-enumeration"></a>SCRIPTGCTYPE 枚举
若要执行的垃圾回收的类型。 在中使用[IActiveScriptGarbageCollector::CollectGarbage](../../winscript/reference/iactivescriptgarbagecollector-collectgarbage.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum tagSCRIPTGCTYPE {    SCRIPTGCTYPE_NORMAL           = 0,    SCRIPTGCTYPE_EXHAUSTIVE       = 1,} SCRIPTGCTYPE;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|||  
|-|-|  
|SCRIPTGCTYPE_NORMAL|执行常规垃圾回收。 整数值为 0。|  
|SCRIPTGCTYPE_EXHAUSTIVE|执行操作的详尽的垃圾回收。 整数值为 1。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)