---
title: IEnumDebugExtendedPropertyInfo 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo interface
ms.assetid: 316d5aa7-c949-48fc-89c1-239f00566cae
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8ceae13f2a785a0920598fa79b237a9c8ae1da1c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72568929"
---
# <a name="ienumdebugextendedpropertyinfo-interface"></a>IEnumDebugExtendedPropertyInfo 接口
枚举 `ExtendedDebugPropertyInfo` 结构。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示 `IEnumDebugExtendedPropertyInfo` 的方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugExtendedPropertyInfo::Clone](../../winscript/reference/ienumdebugextendedpropertyinfo-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[IEnumDebugExtendedPropertyInfo::GetCount](../../winscript/reference/ienumdebugextendedpropertyinfo-getcount.md)|获取枚举器中 `ExtendedDebugPropertyInfo` 结构的数目。|  
|[IEnumDebugExtendedPropertyInfo::Next](../../winscript/reference/ienumdebugextendedpropertyinfo-next.md)|检索枚举序列中指定数目的 `ExtendedDebugPropertyInfo` 结构。|  
|[IEnumDebugExtendedPropertyInfo::Skip](../../winscript/reference/ienumdebugextendedpropertyinfo-skip.md)|跳过枚举序列中指定数目的 `ExtendedDebugPropertyInfo` 结构。|  
|[IEnumDebugExtendedPropertyInfo::Reset](../../winscript/reference/ienumdebugextendedpropertyinfo-reset.md)|将枚举序列重置到开头。|  
  
## <a name="requirements"></a>要求  
 标头： dbgprop  
  
## <a name="see-also"></a>请参阅  
 [ExtendedDebugPropertyInfo 结构](../../winscript/reference/extendeddebugpropertyinfo-structure.md)