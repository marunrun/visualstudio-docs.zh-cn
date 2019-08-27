---
title: IActiveScriptAuthorProcedure::ParseProcedureText | Microsoft Docs
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
ms.openlocfilehash: c513b105a483d0f80510dff9c91fa2c3f09e0523
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955154"
---
# <a name="iactivescriptauthorprocedureparseproceduretext"></a>IActiveScriptAuthorProcedure::ParseProcedureText
分析代码过程中，将代码过程的文本添加到创作引擎，该脚本并创建`IScriptEntry`对应于代码过程的对象。  
  
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
 [in]要分析的脚本文本。  
  
 `pszFormalParams`  
 [in]用于该过程的正式参数名称的地址。 参数名称必须由脚本创作引擎适当的分隔符分隔。 名称不应括在括号中。  
  
 `pszProcedureName`  
 [in]要分析的过程名称的地址。  
  
 `pszItemName`  
 [in]包含的项名称的缓冲区地址与`IScriptEntry`对象。  
  
 `pszDelimiter`  
 [in]最终的脚本块分隔符的地址。 当`pszCode`进行分析的文本流，从主机通常使用分隔符 （如两个单引号），来检测脚本块的末尾。 如果没有分隔符标记的脚本块的结尾，此参数设置为 NULL。  
  
 `dwCookie`  
 [in]与新关联应用程序定义的值`IScriptEntry`对象。  
  
 `dwFlags`  
 [in]不使用。  
  
 `pdispFor`  
 [in]不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 当前[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]引擎不实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthorProcedure 接口](../../winscript/reference/iactivescriptauthorprocedure-interface.md)