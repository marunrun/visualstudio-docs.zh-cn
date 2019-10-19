---
title: IActiveScriptGarbageCollector：： CollectGarbage |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 75f77c49-2190-4d49-a3e0-9dcf847c502b
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0539ed2cb3540cf33ceaaa15827c3ca08c156698
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573586"
---
# <a name="iactivescriptgarbagecollectorcollectgarbage"></a>IActiveScriptGarbageCollector::CollectGarbage
活动脚本宿主调用此方法来启动垃圾回收。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CollectGarbage(        SCRIPTGCTYPE scriptgctype    );  
```  
  
#### <a name="parameters"></a>参数  
 `scriptgctype`  
 中[SCRIPTGCTYPE 枚举](../../winscript/reference/scriptgctype-enumeration.md)，它指定是要执行正常还是穷举垃圾回收。  
  
## <a name="return-value"></a>返回值  
 返回 HRESULT。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptGarbageCollector 接口](../../winscript/reference/iactivescriptgarbagecollector-interface.md)