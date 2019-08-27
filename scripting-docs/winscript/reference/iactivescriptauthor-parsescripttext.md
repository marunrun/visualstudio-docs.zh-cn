---
title: IActiveScriptAuthor::ParseScriptText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.ParseScriptText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::ParseScriptText
ms.assetid: ebe212e8-6789-423d-ad22-92be984dc7ad
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fe6870f3b19c5727fdbea0418b8373b990cb671a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955076"
---
# <a name="iactivescriptauthorparsescripttext"></a>IActiveScriptAuthor::ParseScriptText
分析脚本文本、 将文本添加到创作引擎，该脚本并创建`IScriptEntry`对应于脚本块的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseScriptText(  
   LPCOLESTR pszCode,  
   LPCOLESTR pszItemName,  
   LPCOLESTR pszDelimiter,  
   DWORD dwCookie,  
   DWORD dwFlags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCode`  
 [in]要分析的脚本文本。  
  
 `pszItemName`  
 [in]包含与脚本块关联的项名称的缓冲区地址。  
  
 `pszDelimiter`  
 [in]最终的脚本块分隔符的地址。 当`pszCode`进行分析的文本流，从主机通常使用分隔符 （如两个单引号），来检测脚本块的末尾。 如果没有定界符来标识脚本块的末尾，此参数设置为 NULL。  
  
 `dwCookie`  
 [in]与新关联应用程序定义的值`IScriptEntry`对象。  
  
 `dwFlags`  
 [in]不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)