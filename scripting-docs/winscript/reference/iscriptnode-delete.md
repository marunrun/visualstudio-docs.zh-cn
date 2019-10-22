---
title: IScriptNode：:D e) |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.Delete
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::Delete
ms.assetid: 6765ff80-a9a8-40a3-a669-7fcc284c87af
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c3522e5543d333443de5b1287c994bf29de51c9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576300"
---
# <a name="iscriptnodedelete"></a>IScriptNode::Delete
删除此对象树。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Delete();  
```  
  
#### <a name="parameters"></a>参数  
 方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 调用 `Delete` 方法后， [IScriptNode：： Alive](../../winscript/reference/iscriptnode-alive.md)方法应指示脚本节点处于非活动状态。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)