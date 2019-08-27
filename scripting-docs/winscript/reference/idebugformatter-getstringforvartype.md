---
title: IDebugFormatter::GetStringForVarType |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugFormatter.GetStringForVarType
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugFormatter::GetStringForVarType
ms.assetid: 1c1a0499-ca57-47e0-8367-fdb4c902bca3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3d83df97ac9cb6c38d989470b71da93aceb5d50b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979209"
---
# <a name="idebugformattergetstringforvartype"></a>IDebugFormatter::GetStringForVarType
返回一个字符串，表示给定的 VARTYPE 值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetStringForVarType(  
   VARTYPE    vt,  
   TYPEDESC*  ptdescArrayType,  
   BSTR*      pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `vt`  
 [in]VARTYPE 无法表示为一个字符串。  
  
 `ptdescArrayType`  
 [in]描述类型的结构数组。  
  
 `pbstr`  
 [out]字符串，表示`vt`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 该方法返回一个字符串，表示给定的 VARTYPE 值。  
  
## <a name="see-also"></a>请参阅  
 [IDebugFormatter 接口](../../winscript/reference/idebugformatter-interface.md)