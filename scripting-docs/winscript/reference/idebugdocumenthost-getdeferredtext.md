---
title: 'Idebugdocumenthost:: Getdeferredtext |Microsoft Docs'
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
ms.openlocfilehash: 3e5800a6de15d2d59208022fa44d3c2f4c931e14
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446569"
---
# <a name="idebugdocumenthostgetdeferredtext"></a>IDebugDocumentHost::GetDeferredText
返回添加的使用的字符范围`IDebugDocumentHelper::AddDeferredText`方法，请在原始主机文档。  
  
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
 [in]表示文本的起始位置的主机定义的 cookie。  
  
 `pcharText`  
 [in、 out]字符文本缓冲区。 此方法不返回字符，如果此参数为`NULL`。  
  
 `pstaTextAttr`  
 [in、 out]字符属性缓冲区。 此方法不返回特性，如果此参数为`NULL`。  
  
 `pcNumChars`  
 [in、 out]指示返回的字符/属性的实际数目。 此参数必须设置为零之前调用此方法。  
  
 `cMaxChars`  
 [in]要返回的字符数目上限。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|未实现方法。|  
  
## <a name="remarks"></a>备注  
 此方法可能会返回`E_NOTIMPL`，如果主机不会调用`IDebugDocumentHelper::AddDeferredText`。  
  
> [!NOTE]
> 此方法返回从原始文档的文本。 主机不会不跟踪的编辑或对文档的其他更改。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)   
 [IDebugDocumentHelper::AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)