---
title: IApplicationDebuggerUI::BringDocumentToTop | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebuggerUI.BringDocumentToTop
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebuggerUI::BringDocumentToTop
ms.assetid: ef5fe1e7-4381-4409-a0d7-58f993abe84e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a8a88b44f609113670259492eb82491b16004d29
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991129"
---
# <a name="iapplicationdebuggeruibringdocumenttotop"></a>IApplicationDebuggerUI::BringDocumentToTop
用户界面将包含到在调试器中的顶部指定的调试文档的窗口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT BringDocumentToTop(  
   IDebugDocumentText*  pddt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pddt`  
 [in]调试文档，以在调试器用户界面中将放在顶部。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_INVALIDARG`|不知道该文档。|  
  
## <a name="remarks"></a>备注  
 此方法将包含到在调试器中的顶部指定的调试文档的窗口的用户界面。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebuggerUI 接口](../../winscript/reference/iapplicationdebuggerui-interface.md)