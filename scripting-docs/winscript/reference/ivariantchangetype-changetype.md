---
title: IVariantChangeType::ChangeType |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IVariantChangeType.ChangeType
apilocation:
- scrobj.dll
helpviewer_keywords:
- IVariantChangeType::ChangeType
ms.assetid: 52374764-c42e-49af-a219-ee00c535a118
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 81ed0a8502e9b0cfc53725621d477d34ee5010ea
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945628"
---
# <a name="ivariantchangetypechangetype"></a>IVariantChangeType::ChangeType
采用变量值并创建具有指定类型的新变体。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ChangeType(  
   VARIANT*  pvarDst,  
   VARIANT*  pvarSrc,  
   LCID  lcid,  
   VARTYPE  vtNew  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvarDst`  
 [in、 out]以包含所表示的值的变体`pvarSrc`，但指定的类型与`vtNew`。  
  
 `pvarSrc`  
 [in]要将更改为新类型的变体值。  
  
 `lcid`  
 [in]要转换到或从字符串自变量时使用的区域设置上下文。  
  
 `vtNew`  
 [in]指定的类型`pvarDst`成为。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 `pvarDst`和`pvarSrc`参数可能是相等的在这种情况下会覆盖原始值。 此方法将传递`pvarDst`到`VariantClear`函数，并由此`pvarDst`应为有效的值进行初始化。  
  
## <a name="see-also"></a>请参阅  
 [IVariantChangeType 接口](../../winscript/reference/ivariantchangetype-interface.md)