---
title: IEnumDebugCodeContexts::Clone | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugCodeContexts.Clone
apilocation:
- jscript.dll
helpviewer_keywords:
- IEnumDebugCodeContexts::Clone
ms.assetid: eaad6af9-4a0a-49c9-8f73-bccaa42b235c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a08c65a7be5ed0b6394ef5e0aab284a03a52a240
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951456"
---
# <a name="ienumdebugcodecontextsclone"></a>IEnumDebugCodeContexts::Clone
创建一个包含与当前枚举数相同的状态的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Clone(  
   IEnumDebugCodeContexts**  ppescc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppescc`  
 [out]返回`IEnumDebugCodeContexts`接口的枚举器的克隆。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法创建一个包含与当前枚举数相同的状态的枚举器。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugCodeContexts 接口](../../winscript/reference/ienumdebugcodecontexts-interface.md)