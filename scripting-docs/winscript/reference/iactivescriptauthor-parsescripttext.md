---
title: IActiveScriptAuthor：:P arseScriptText |Microsoft Docs
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
ms.openlocfilehash: 90d5ab0fa700ed29b5fb37b1c48617cedec871b9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576142"
---
# <a name="iactivescriptauthorparsescripttext"></a>IActiveScriptAuthor::ParseScriptText
分析脚本文本，将文本添加到脚本创作引擎，并创建与脚本块对应的 `IScriptEntry` 对象。  
  
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
 中要分析的脚本文本。  
  
 `pszItemName`  
 中包含与脚本块关联的项名称的缓冲区地址。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 当从文本流分析 `pszCode` 时，主机通常使用分隔符（如两个单引号）来检测脚本块的结尾。 如果没有分隔符用于标识脚本块的末尾，则将此参数设置为 NULL。  
  
 `dwCookie`  
 中与新的 `IScriptEntry` 对象关联的应用程序定义的值。  
  
 `dwFlags`  
 中不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)