---
title: IDebugApplicationNode::Attach |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNode.Attach
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationNode::Attach
ms.assetid: f4aad4ae-5bb0-4b5e-8f70-912a677f8f7a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c41d06c116c7c15ad308ce2ace837ea01d90ab1d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990487"
---
# <a name="idebugapplicationnodeattach"></a>IDebugApplicationNode::Attach
将此应用程序节点添加到指定的项目树。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Attach(  
   IDebugApplicationNode*  pdanParent  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdanParent`  
 [in]此应用程序节点都是要添加到项目树。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将此应用程序节点添加到项目树中，使用`pdanParent`作为父级。 如果`pdanParent`是`NULL`，此应用程序节点将作为顶级节点。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode::Detach](../../winscript/reference/idebugapplicationnode-detach.md)   
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)