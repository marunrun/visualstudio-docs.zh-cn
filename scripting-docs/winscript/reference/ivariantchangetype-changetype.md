---
title: IVariantChangeType：： ChangeType |Microsoft Docs
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
ms.openlocfilehash: 406d5d8486b3016f0105b7bd8bf231db0e1e9613
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571778"
---
# <a name="ivariantchangetypechangetype"></a>IVariantChangeType::ChangeType
采用变量值并创建具有指定类型的新变量。  
  
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
 [in，out]一个变量，包含由 `pvarSrc` 表示的值，但具有 `vtNew` 指定的类型。  
  
 `pvarSrc`  
 中要更改为新类型的变量值。  
  
 `lcid`  
 中在将参数转换为字符串或从字符串转换时要使用的区域设置上下文。  
  
 `vtNew`  
 中指定要成为 `pvarDst` 的类型。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 @No__t_0 和 `pvarSrc` 参数可能相等，在这种情况下，将覆盖原始值。 此方法将 `pvarDst` 传递到 `VariantClear` 函数，因此 `pvarDst` 应初始化为有效的值。  
  
## <a name="see-also"></a>请参阅  
 [IVariantChangeType 接口](../../winscript/reference/ivariantchangetype-interface.md)