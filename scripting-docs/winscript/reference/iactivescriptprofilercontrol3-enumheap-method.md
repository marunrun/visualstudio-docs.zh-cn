---
title: IActiveScriptProfilerControl3::EnumHeap 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2799d06d-20dd-4c12-9646-554c0ea3606e
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6120b8fdd913b4acee2e3ee6774d770aa75b1f5a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992957"
---
# <a name="iactivescriptprofilercontrol3enumheap-method"></a>IActiveScriptProfilerControl3::EnumHeap 方法
返回的接口 ([IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)) 可用于循环访问关联的脚本引擎的上下文中的 GC 堆对象。  
  
 可以调用此方法在调试或发布模式。 UI 线程处于空闲状态时，应调用此方法。 调用该方法后，应执行任何操作的脚本引擎除外[iactivescriptprofilerheapenum:: Next 方法](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)直到[iactivescriptprofilerheapenum:: Next 方法](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)，则返回 S_FALSE 或[IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)释放接口指针。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumHeap([out] IActiveScriptProfilerHeapEnum** ppEnum);  
```  
  
#### <a name="parameters"></a>参数  
 ppEnum  
 [out]返回[IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)。  
  
## <a name="return-value"></a>返回值  
 HRESULT。