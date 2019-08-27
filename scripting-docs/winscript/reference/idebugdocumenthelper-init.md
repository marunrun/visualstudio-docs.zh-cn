---
title: 'Idebugdocumenthelper:: Init |Microsoft Docs'
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
ms.openlocfilehash: 3b399f51fc042aa1ed297ab30a7bf2c9bc4befca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000988"
---
# <a name="idebugdocumenthelperinit"></a>IDebugDocumentHelper::Init
`Init`方法初始化使用名称和初始属性的调试文档帮助程序。  
  
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
 [in]与此文档关联的调试应用程序。  
  
 `pszShortName`  
 [in]包含文档的短名称的以 null 结尾的字符串。  
  
 `pszLongName`  
 [in]包含文档的长名称的以 null 结尾的字符串。  
  
 `docAttr`  
 [in]指定文本文档属性。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法初始化使用名称和初始属性的调试文档帮助程序。  
  
 本文档不会显示在树中，直到`IDebugDocumentHelper::Attach`调用。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper::Attach](../../winscript/reference/idebugdocumenthelper-attach.md)   
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [TEXT_DOC_ATTR 常量](../../winscript/reference/text-doc-attr-constants.md)