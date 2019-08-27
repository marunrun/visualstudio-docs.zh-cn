---
title: IScriptEntry::GetSignature | Microsoft Docs
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
ms.openlocfilehash: 70cc1939ae4eb1e3c58d31b3d42b7f1b4603ce9e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787788"
---
# <a name="iscriptentrygetsignature"></a>IScriptEntry::GetSignature
返回类型信息`IScriptEntry`函数对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSignature(  
   ITypeInfo          **ppti  
   ULONG              *piMethod  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppti`  
 [out]键入与此相关联的信息`IScriptEntry`函数对象。  
  
 `piMethod`  
 [out]中的方法索引`ITypeInfo`对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 使用设置类型信息[IScriptEntry::SetSignature](../../winscript/reference/iscriptentry-setsignature.md)或[IScriptNode::CreateChildHandler](../../winscript/reference/iscriptnode-createchildhandler.md)。 此外可以通过基于内部函数表示形式的条目生成类型信息。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)