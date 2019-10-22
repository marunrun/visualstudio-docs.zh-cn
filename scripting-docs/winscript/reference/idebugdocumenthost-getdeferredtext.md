---
title: IDebugDocumentHost：： GetDeferredText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetDeferredText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetDeferredText
ms.assetid: 527da666-fef5-4db3-a319-e68d466a7721
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 273b4eb52b7263d34c347dff3a00479945b809df
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569420"
---
# <a name="idebugdocumenthostgetdeferredtext"></a>IDebugDocumentHost::GetDeferredText
返回在原始宿主文档中使用 `IDebugDocumentHelper::AddDeferredText` 方法添加的一系列字符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDeferredText(  
   DWORD              dwTextStartCookie,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwTextStartCookie`  
 中主机定义的 cookie，表示文本的起始位置。  
  
 `pcharText`  
 [in，out]字符文本缓冲区。 如果 `NULL` 此参数，则此方法不返回字符。  
  
 `pstaTextAttr`  
 [in，out]字符特性缓冲区。 如果 `NULL` 此参数，则此方法不返回特性。  
  
 `pcNumChars`  
 [in，out]指示返回的字符/属性的实际数量。 在调用此方法之前，此参数必须设置为零。  
  
 `cMaxChars`  
 中要返回的最大字符数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|未实现该方法。|  
  
## <a name="remarks"></a>备注  
 如果主机未调用 `IDebugDocumentHelper::AddDeferredText`，则此方法可能会返回 `E_NOTIMPL`。  
  
> [!NOTE]
> 此方法返回原始文档中的文本。 宿主不跟踪对文档进行的编辑或其他更改。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)   
 [IDebugDocumentHelper：： AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)    
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)