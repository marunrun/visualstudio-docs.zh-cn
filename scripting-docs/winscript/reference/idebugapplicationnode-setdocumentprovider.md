---
title: IDebugApplicationNode：： SetDocumentProvider |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNode.SetDocumentProvider
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationNode::SetDocumentProvider
ms.assetid: 7cb587ca-d84e-4b5e-9b94-e973cca55a03
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2dd1588ed1bb365e88bb3b09ee5093f15ac7a161
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574827"
---
# <a name="idebugapplicationnodesetdocumentprovider"></a>IDebugApplicationNode::SetDocumentProvider
设置此应用程序节点的文档提供程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetDocumentProvider(  
   IDebugDocumentProvider*  pddp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pddp`  
 中此应用程序节点的文档提供程序。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法设置此应用程序节点的文档提供程序。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)