---
title: IDebugApplication::CreateApplicationNode | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.CreateApplicationNode
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::CreateApplicationNode
ms.assetid: 1a1414f6-df14-4c56-b39a-8384cf16174a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 02a15a67d8f8b6171e9f5893c7f8cd15f79776b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991020"
---
# <a name="idebugapplicationcreateapplicationnode"></a>IDebugApplication::CreateApplicationNode
创建一个新的应用程序节点与特定文档提供程序相关联。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateApplicationNode(  
   IDebugApplicationNode**  ppdanNew  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppdanNew`  
 [out]与此文档提供程序关联的应用程序节点。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 新的应用程序节点不可见，直到它附加到父节点。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)