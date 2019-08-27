---
title: IDebugExtendedProperty 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugExtendedProperty interface
ms.assetid: e92ea064-0d92-44cf-bb9f-abda783d84be
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c1e042f75cf0ab0d8c4807c0c0db6ce04e8423f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945869"
---
# <a name="idebugextendedproperty-interface"></a>IDebugExtendedProperty 接口
扩展了`IDebugProperty`接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了继承的方法之外`IDebugProperty`，此接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugExtendedProperty::GetExtendedPropertyInfo](../../winscript/reference/idebugextendedproperty-getextendedpropertyinfo.md)|获取`ExtendedDebugPropertyInfo`描述此 `IDebugExtendedProperty``.`|  
|[IDebugExtendedProperty::EnumExtendedMembers](../../winscript/reference/idebugextendedproperty-enumextendedmembers.md)|枚举扩展属性的成员。|  
  
## <a name="requirements"></a>要求  
 标头： dbgprop.h  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)