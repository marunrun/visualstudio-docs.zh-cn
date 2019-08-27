---
title: IDebugDocumentHelper::SetDefaultTextAttr |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.SetDefaultTextAttr
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::SetDefaultTextAttr
ms.assetid: 019a4191-0019-4376-bf70-89b33e7369de
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 09f75e6f09639520462d5ef3983d67333097f76e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62948949"
---
# <a name="idebugdocumenthelpersetdefaulttextattr"></a>IDebugDocumentHelper::SetDefaultTextAttr
设置要用于不是将脚本块中的文本的默认特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetDefaultTextAttr(  
   SOURCE_TEXT_ATTR  staTextAttr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `staTextAttr`  
 默认源文本特性。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法更改了默认属性，除非脚本块外的文本的默认属性是 SOURCETEXT_ATTR_NONSOURCE。 用户界面可以使用此信息将标记为只读的脚本块之外的文本。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)