---
title: IDebugDocumentHelper：： Init |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.Init
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::Init
ms.assetid: 1dd5a01f-0779-4109-8c6c-f16f5a3835bf
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 13e6379052707aa44c0fa52f4cb30db2c4c4fa99
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576865"
---
# <a name="idebugdocumenthelperinit"></a>IDebugDocumentHelper::Init
`Init` 方法使用 name 和初始属性初始化调试文档帮助程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Init(  
   IDebugApplication*  pda,  
   LPCOLESTR           pszShortName,  
   LPCOLESTR           pszLongName,  
   TEXT_DOC_ATTR       docAttr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pda`  
 中与此文档关联的调试应用程序。  
  
 `pszShortName`  
 中一个以 null 结尾的字符串，其中包含文档的短名称。  
  
 `pszLongName`  
 中一个以 null 结尾的字符串，其中包含文档的长名称。  
  
 `docAttr`  
 中指定文本文档属性。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法使用名称和初始属性初始化调试文档帮助程序。  
  
 在调用 `IDebugDocumentHelper::Attach` 之前，此文档不会显示在树中。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDocumentHelper::Attach](../../winscript/reference/idebugdocumenthelper-attach.md)   
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [TEXT_DOC_ATTR 常量](../../winscript/reference/text-doc-attr-constants.md)