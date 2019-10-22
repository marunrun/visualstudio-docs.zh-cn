---
title: IEnumDebugPropertyInfo 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumDebugPropertyInfo interface
ms.assetid: c5eea4da-8414-408a-a8f6-6a9ca8745868
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0ce4f5a114629a473df99b583c77ae7747bcd339
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574187"
---
# <a name="ienumdebugpropertyinfo-interface"></a>IEnumDebugPropertyInfo 接口
枚举 `DebugPropertyInfo` 结构。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示 `IEnumDebugPropertyInfo` 的方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugPropertyInfo::Next](../../winscript/reference/ienumdebugpropertyinfo-next.md)|检索枚举序列中指定数目的 `DebugPropertyInfo` 结构。|  
|[IEnumDebugPropertyInfo::Skip](../../winscript/reference/ienumdebugpropertyinfo-skip.md)|跳过枚举序列中指定数目的 `DebugPropertyInfo` 结构。|  
|[IEnumDebugPropertyInfo::Reset](../../winscript/reference/ienumdebugpropertyinfo-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugPropertyInfo::Clone](../../winscript/reference/ienumdebugpropertyinfo-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[IEnumDebugPropertyInfo::GetCount](../../winscript/reference/ienumdebugpropertyinfo-getcount.md)|获取枚举器中 `DebugPropertyInfo` 结构的数目。|  
  
## <a name="requirements"></a>要求  
 标头： dbgprop  
  
## <a name="see-also"></a>请参阅  
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)