---
title: IScriptEntry：： GetSignature |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetSignature
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetSignature
ms.assetid: 8cbf37ac-b14c-4e15-a613-06f34857da9b
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7b07ac64ce7e427a793f0af0db9a7905441d39b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575419"
---
# <a name="iscriptentrygetsignature"></a>IScriptEntry::GetSignature
返回 `IScriptEntry` 函数对象的类型信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSignature(  
   ITypeInfo          **ppti  
   ULONG              *piMethod  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppti`  
 弄键入与此 `IScriptEntry` 函数对象关联的信息。  
  
 `piMethod`  
 弄@No__t_0 对象中的方法索引。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 使用[IScriptEntry：： SetSignature](../../winscript/reference/iscriptentry-setsignature.md)或[IScriptNode：： CreateChildHandler](../../winscript/reference/iscriptnode-createchildhandler.md)设置类型信息。 还可以根据内部函数表示形式，通过项生成类型信息。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)