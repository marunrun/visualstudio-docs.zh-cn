---
title: IEnumDebugPropertyInfo Interface | Microsoft Docs
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
ms.openlocfilehash: 736bea847908e3c70d6caf2f8e41af38608f4f23
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963424"
---
# <a name="ienumdebugpropertyinfo-interface"></a>IEnumDebugPropertyInfo 接口
枚举`DebugPropertyInfo`结构。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugPropertyInfo`。  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugPropertyInfo::Next](../../winscript/reference/ienumdebugpropertyinfo-next.md)|检索指定的数目的`DebugPropertyInfo`枚举序列中的结构。|  
|[IEnumDebugPropertyInfo::Skip](../../winscript/reference/ienumdebugpropertyinfo-skip.md)|跳过指定的数目的`DebugPropertyInfo`枚举序列中的结构。|  
|[IEnumDebugPropertyInfo::Reset](../../winscript/reference/ienumdebugpropertyinfo-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugPropertyInfo::Clone](../../winscript/reference/ienumdebugpropertyinfo-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[IEnumDebugPropertyInfo::GetCount](../../winscript/reference/ienumdebugpropertyinfo-getcount.md)|获取数`DebugPropertyInfo`枚举器中的结构。|  
  
## <a name="requirements"></a>要求  
 标头： dbgprop.h  
  
## <a name="see-also"></a>请参阅  
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)