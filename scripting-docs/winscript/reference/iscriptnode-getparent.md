---
title: IScriptNode::GetParent |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetParent
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetParent
ms.assetid: 0fb813f6-ab94-46b2-b0cf-ef5d1cd38ae4
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1c990b5ba5c3d03d319e0eeced282c92cfbb5281
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786851"
---
# <a name="iscriptnodegetparent"></a>IScriptNode::GetParent
返回`IScriptNode`是父对象的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetParent(  
   IScriptNode       **ppsnParent  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppsnParent`  
 [out]一个变量来接收指向指针的地址`IScriptNode`接口的父实例。  
  
 如果类实现`IScriptEntry`或`IScriptScriptlet`、`IScriptNode`返回对象。  
  
 如果类实现`IScriptNode`（表示网页上），则返回 NULL。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)