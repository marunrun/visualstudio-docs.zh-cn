---
title: IDebugApplicationNode：： Attach |Microsoft Docs
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
ms.openlocfilehash: 30d4e189ec878def1cfd88517654955cd2d1aa12
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574788"
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
 中要在其中添加此应用程序节点的项目树。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法使用 `pdanParent` 作为父项，将此应用程序节点添加到项目树中。 如果 `NULL` `pdanParent`，则此应用程序节点将为顶级节点。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode：:D etach](../../winscript/reference/idebugapplicationnode-detach.md)    
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)