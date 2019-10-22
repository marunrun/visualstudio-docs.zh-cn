---
title: IScriptNode：： System.windows.media.visualtreehelper.getchild |Microsoft Docs
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
ms.openlocfilehash: 27ddde527be1ea4148e4166581ab2cb1a71d15f7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573554"
---
# <a name="iscriptnodegetchild"></a>IScriptNode::GetChild
返回位于节点中指定索引处的子级。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetChild(  
   ULONG              isn,  
   IScriptNode        **ppsn  
);  
```  
  
#### <a name="parameters"></a>参数  
 `isn`  
 中父中子级的索引。  
  
 `ppsn`  
 弄一个变量的地址，该变量接收指向子实例的 `IScriptNode` 接口的指针。  
  
 对于表示网页的 `IScriptNode` 对象，此参数将返回包含脚本块的对象。  
  
 对于指定脚本块的 `IScriptEntry` 对象，此参数返回指定函数的对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 对于指定函数对象和 `IScriptScriptlet` 对象的 `IScriptEntry` 对象，此方法失败，因为没有子项。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)