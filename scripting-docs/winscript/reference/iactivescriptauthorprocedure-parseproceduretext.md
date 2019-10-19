---
title: IActiveScriptAuthorProcedure：:P arseProcedureText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthorProcedure.ParseProcedureText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthorProcedure::ParseProcedureText
ms.assetid: cb6c29c5-c749-48d7-a6a8-ccbf0f9119ec
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 11a34843f30274ec78f1652c5ed5cd4dbcf2884a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572815"
---
# <a name="iactivescriptauthorprocedureparseproceduretext"></a>IActiveScriptAuthorProcedure::ParseProcedureText
分析代码过程，将代码过程的文本添加到脚本创作引擎中，并创建一个与代码过程相对应的 `IScriptEntry` 对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseProcedureText(  
   LPCOLESTR   pszCode,  
   LPCOLESTR   pszFormalParams,  
   LPCOLESTR   pszProcedureName,  
   LPCOLESTR   pszItemName,  
   LPCOLESTR   pszDelimiter,  
   DWORD       dwCookie,  
   DWORD       dwFlags,  
   IDispatch   *pdispFor  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCode`  
 中要分析的脚本文本。  
  
 `pszFormalParams`  
 中过程的形参名称的地址。 参数名称必须用适用于脚本创作引擎的分隔符分隔。 名称不应括在括号中。  
  
 `pszProcedureName`  
 中要分析的过程名称的地址。  
  
 `pszItemName`  
 中包含与 `IScriptEntry` 对象关联的项名称的缓冲区地址。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 当从文本流分析 `pszCode` 时，主机通常使用分隔符（如两个单引号）来检测脚本块的结尾。 如果没有分隔符来标记脚本块的末尾，则将此参数设置为 NULL。  
  
 `dwCookie`  
 中与新的 `IScriptEntry` 对象关联的应用程序定义的值。  
  
 `dwFlags`  
 中不使用。  
  
 `pdispFor`  
 中不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 当前 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 引擎未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthorProcedure 接口](../../winscript/reference/iactivescriptauthorprocedure-interface.md)