---
title: 'Ijsdebugproperty:: Getmembers 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugProperty.GetMembers
apilocation:
- jscript9diag.dll
ms.assetid: a32b5372-d9cb-4b9a-9bc2-81b5e1df365c
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3be31a0f02869ea740809fb68dbddf48843b2f3e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62793664"
---
# <a name="ijsdebugpropertygetmembers-method"></a>IJsDebugProperty::GetMembers 方法
获取此对象的成员。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetMembers(  
   JS_PROPERTY_MEMBERS members,  
   IJsEnumDebugProperty **ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `members`  
 [in]若要指定的成员信息中包含的内容的标志。  
  
 `ppEnum`  
 [out]对象的成员。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugProperty 接口](../../winscript/reference/ijsdebugproperty-interface.md)