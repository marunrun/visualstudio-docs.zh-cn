---
title: IDebugDocumentHelper：： AddDeferredText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.AddDeferredText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::AddDeferredText
ms.assetid: 9463cfb0-76cc-45ee-b32c-f37dce2b2e0e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1aae73e44059b1f07fa4cb54f40cdcd12e564a8f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577038"
---
# <a name="idebugdocumenthelperadddeferredtext"></a>IDebugDocumentHelper::AddDeferredText
通知帮助器：给定文本可用，但不提供字符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddDeferredText(  
   ULONG  cChars,  
   DWORD  dwTextStartCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cChars`  
 中要添加的（Unicode）字符数。  
  
 `dwTextStartCookie`  
 中主机定义的 cookie，表示文本的起始位置。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|方法失败。|  
  
## <a name="remarks"></a>备注  
 此方法允许宿主提供要在需要时添加的字符，同时允许帮助者生成准确的通知和大小信息。 `dwTextStartCookie` 参数是由宿主定义的 cookie，它表示文本的起始位置。 对 `IDebugDocumentText::GetText` 的后续调用必须提供此 cookie。 例如，在表示 DBCS 中文本的主机中，cookie 可以是字节偏移量。  
  
 假设单个调用 `IDebugDocumentText::GetText` 可以从多个调用中获取字符 `AddDeferredText`。 帮助程序类还可能会要求多次延迟字符。  
  
> [!NOTE]
> 不应将对 `AddDeferredText` 的调用与 `AddUnicodeText` 或 `AddDBCSText`的调用混合。 如果出现这种情况，则返回 `E_FAIL`。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)   
 [IDebugDocumentHelper::AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)