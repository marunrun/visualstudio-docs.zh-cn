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
ms.openlocfilehash: 5f28e0ddd3764b3810d25bfbb9403c391c1bfd54
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238447"
---
# <a name="scriptgctype-enumeration"></a>SCRIPTGCTYPE 枚举
要执行的垃圾回收的类型。 在 [IActiveScriptGarbageCollector：： CollectGarbage](../../winscript/reference/iactivescriptgarbagecollector-collectgarbage.md) 方法中使用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum tagSCRIPTGCTYPE {    SCRIPTGCTYPE_NORMAL           = 0,    SCRIPTGCTYPE_EXHAUSTIVE       = 1,} SCRIPTGCTYPE;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|垃圾回收类型|  
|-|-|  
|SCRIPTGCTYPE_NORMAL|执行正常的垃圾回收。 整数值为0。|  
|SCRIPTGCTYPE_EXHAUSTIVE|进行详尽的垃圾回收。 整数值为1。|  
  
## <a name="see-also"></a>另请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)