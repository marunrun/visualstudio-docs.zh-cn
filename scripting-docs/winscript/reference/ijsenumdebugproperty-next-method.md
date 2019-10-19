---
title: IJsEnumDebugProperty：： Next 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsEnumDebugProperty.Next
apilocation:
- jscript9diag.dll
ms.assetid: 9fad1893-483a-440c-88c1-469494212300
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 48c4506d783093395b2d88b7a71d56e3a89d24e8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573992"
---
# <a name="ijsenumdebugpropertynext-method"></a>IJsEnumDebugProperty::Next 方法
读取此对象的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG count,  
   IJsDebugProperty **ppDebugProperty,  
   ULONG *pActualCount  
);  
```  
  
#### <a name="parameters"></a>参数  
 `count`  
 中要读取的属性的数目。  
  
 `ppDebugProperty`  
 弄表示属性浏览器的对象。  
  
 `pActualCount`  
 弄对象的实际属性数。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsEnumDebugProperty 接口](../../winscript/reference/ijsenumdebugproperty-interface.md)