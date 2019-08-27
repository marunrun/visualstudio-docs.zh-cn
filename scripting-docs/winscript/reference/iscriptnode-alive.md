---
title: IScriptNode::Alive |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.Alive
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::Alive
ms.assetid: d2755c83-e9b9-4c0a-acb7-25b554fc9fe8
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: da0a55d26b5ab643670ba7ed51e576eeb89d8b98
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787168"
---
# <a name="iscriptnodealive"></a>IScriptNode::Alive
指示对象是否仍处于活动状态。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Alive();  
```  
  
#### <a name="parameters"></a>参数  
 该方法采用任何参数。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|脚本节点仍处于活动状态。|  
  
## <a name="remarks"></a>备注  
 如果该对象不处于活动状态，组件对象模型 (COM) 从对此方法的调用封送处理代理返回错误。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)