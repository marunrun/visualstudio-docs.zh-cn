---
title: IDebugDocumentTextExternalAuthor：： GetPathName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextExternalAuthor.GetPathName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentTextExternalAuthor::GetPathName
ms.assetid: 445152a1-9cf8-402e-93d6-3d4bf2b81d17
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e876b41ce1bde4defffd11267c6665f9d57da077
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575971"
---
# <a name="idebugdocumenttextexternalauthorgetpathname"></a>IDebugDocumentTextExternalAuthor::GetPathName
返回文档的完整路径和文件名。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetPathName(  
   BSTR*  pbstrLongName,  
   BOOL*  pfIsOriginalFile  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrLongName`  
 弄包含完整路径和文件名的字符串。  
  
 `pfIsOriginalFile`  
 弄布尔值，指示路径和文件名是否引用原始文档。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|无法创建或确定源文件。|  
  
## <a name="remarks"></a>备注  
 此方法返回文档的完整路径和文件名。  
  
 如果 `pfIsOriginalFile` 为 FALSE，则 `pbstrLongName` 中的路径和文件名引用新创建的临时文件。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextExternalAuthor 接口](../../winscript/reference/idebugdocumenttextexternalauthor-interface.md)