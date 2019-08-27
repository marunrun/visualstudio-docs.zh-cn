---
title: IScriptNode::GetChild | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetChild
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetChild
ms.assetid: 8cb3f8b0-958b-40bb-a91a-49a788661861
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 78b5c84c6ed9b3de9593f0d6ff02df93a0e9ba77
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787125"
---
# <a name="iscriptnodegetchild"></a>IScriptNode::GetChild
返回位于指定索引中的节点的子级。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetChild(  
   ULONG              isn,  
   IScriptNode        **ppsn  
);  
```  
  
#### <a name="parameters"></a>参数  
 `isn`  
 [in]子对象的父代中的索引。  
  
 `ppsn`  
 [out]一个变量来接收指向指针的地址`IScriptNode`接口的子实例。  
  
 有关`IScriptNode`表示网页的对象，此参数返回一个对象，包含一个脚本块。  
  
 有关`IScriptEntry`指定脚本块的对象，此参数返回指定的函数的对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 有关`IScriptEntry`指定的函数对象的对象和`IScriptScriptlet`对象，此方法失败，因为没有子条目。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)