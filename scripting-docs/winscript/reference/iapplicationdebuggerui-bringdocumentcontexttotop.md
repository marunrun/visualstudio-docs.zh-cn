---
title: IApplicationDebuggerUI::BringDocumentContextToTop | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebuggerUI.BringDocumentContextToTop
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebuggerUI::BringDocumentContextToTop
ms.assetid: 7844217d-658b-42af-8d10-2714f4eded20
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 596f9357a8553bf6c39140a6948d8ae3085c3210
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991131"
---
# <a name="iapplicationdebuggeruibringdocumentcontexttotop"></a>IApplicationDebuggerUI::BringDocumentContextToTop
引入了包含给定的文档上下文页首调试器用户界面中的窗口和窗口滚动到上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT BringDocumentContextToTop(  
   IDebugDocumentContext*  pddc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pddc`  
 [in]若要在调试器用户界面中将放在顶部的文档上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_INVALIDARG`|指定的上下文`pddc`未知的。|  
  
## <a name="remarks"></a>备注  
 此方法会使其中包含给定的文档上下文中调试器用户界面顶部到窗口，并将窗口滚动到上下文。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebuggerUI 接口](../../winscript/reference/iapplicationdebuggerui-interface.md)