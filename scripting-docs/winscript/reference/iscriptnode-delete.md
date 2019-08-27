---
title: IScriptNode::Delete | Microsoft Docs
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
ms.openlocfilehash: 41bf932b242865b1deac4c61db400f973bd0b00c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787155"
---
# <a name="iscriptnodedelete"></a>IScriptNode::Delete
删除此对象树。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Delete();  
```  
  
#### <a name="parameters"></a>参数  
 该方法采用任何参数。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 之后`Delete`调用方法时， [IScriptNode::Alive](../../winscript/reference/iscriptnode-alive.md)方法应指示该脚本节点未处于活动状态。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)