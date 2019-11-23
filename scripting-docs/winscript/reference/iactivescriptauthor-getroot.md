---
title: IActiveScriptAuthor：： GetRoot |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetRoot
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetRoot
ms.assetid: 8e55a0c0-dd35-43d5-bf6f-e2f59c1e88d1
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ca2aab154d56cd98c3c2acede61f86f725ce9c1b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576190"
---
# <a name="iactivescriptauthorgetroot"></a>IActiveScriptAuthor::GetRoot
返回作者脚本树的 `IScriptNode` 根。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetRoot(  
   IScriptNode        **ppsp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppsp`  
 弄一个变量的地址，该变量接收指向根节点的 `IScriptNode` 接口的指针。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)