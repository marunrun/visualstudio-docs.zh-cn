---
title: IScriptNode::GetCookie |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetCookie
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetCookie
ms.assetid: 007339c6-a73a-4147-b3c0-cc041e467ecd
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b05d184af3ecd6302fc05893600fd7026eeca3ad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787047"
---
# <a name="iscriptnodegetcookie"></a>IScriptNode::GetCookie
返回用于将 scriptlet 与该主机对象相关联的应用程序定义的值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetCookie(  
   DWORD              *pdwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwCookie`  
 [out]有关`IScriptEntry`对象，则返回应用程序定义的 cookie 值。  
  
 有关`IScriptNode`对象，表示网页，返回 0。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)