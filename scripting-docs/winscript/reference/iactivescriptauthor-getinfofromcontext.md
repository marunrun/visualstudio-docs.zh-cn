---
title: IActiveScriptAuthor：： GetInfoFromContext |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetInfoFromContext
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetInfoFromContext
ms.assetid: 9891b095-6eb5-4473-87c0-c2e5cd2afc1a
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 457b2ad1bda3226caf3604e3ccd6b976f01bca83
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576215"
---
# <a name="iactivescriptauthorgetinfofromcontext"></a>IActiveScriptAuthor::GetInfoFromContext
返回代码块中给定字符的类型信息和定位点位置。 这为成员 IntelliSense、全局列表和参数提示提供信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetInfoFromContext(  
   LPCOLESTR  pszCode,  
   ULONG      cchCode,  
   ULONG      ichCurrentPosition,  
   DWORD      dwListTypesRequested,  
   DWORD      *pdwListTypesProvided,  
   ULONG      *pichListAnchorPosition,  
   ULONG      *pichFuncAnchorPosition,  
   MEMBERID   *pmemid,  
   LONG       *piCurrentParameter,  
   IUnknown   **ppunk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCode`  
 中用于生成信息结果的代码块字符串的地址。  
  
 `cchCode`  
 中代码块的长度。  
  
 `ichCurrentPosition`  
 中字符相对于块开头的位置。  
  
 `dwListTypesRequested`  
 中请求的列表类型。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_NOLIST|0x0000|无列表。|  
|SCRIPT_CMPL_MEMBERLIST|0x0001|成员列表。|  
|SCRIPT_CMPL_ENUMLIST|0x0002|枚举列表。|  
|SCRIPT_CMPL_PARAMLIST|0x0004|调用方法参数列表。|  
|SCRIPT_CMPL_GLOBALLIST|0x0008|全局列表。|  
  
 SCRIPT_CMPL_GLOBALLIST 类型被视为默认完成项，可通过将 OR 运算符与其他完成项结合使用来进行组合。 脚本创作引擎首先尝试填充其他完成列表项的类型信息。 如果此操作失败，则引擎将为 SCRIPT_CMPL_GLOBALLIST 填充。  
  
 `pdwListTypesProvided`  
 弄提供的列表的类型。  
  
 `pichListAnchorPosition`  
 弄包含当前位置的上下文的开始索引。 起始索引相对于块的开头。  
  
 仅当 `dwListTypesRequested` 包括 SCRIPT_CMPL_MEMBERLIST、SCRIPT_CMPL_ENUMLIST 或 SCRIPT_CMPL_GLOBALLIST 时，才填充此内容。 对于其他请求的列表类型，结果是不确定的。  
  
 `pichFuncAnchorPosition`  
 弄包含当前位置的函数调用的起始索引。 起始索引相对于块的开头。  
  
 仅当包含当前位置的上下文是函数调用并且 `dwListTypesRequested` 包含 SCRIPT_CMPL_PARAMLIST 时，才填充此内容。 否则，结果为 undefined。  
  
 `pmemid`  
 弄函数的 MEMBERID，由 `IProvideMultipleClassInfo``ppunk` out 参数中的类型定义。  
  
 仅当 `dwListTypesRequested` 包括 SCRIPT_CMPL_PARAMLIST 时，才填充此内容。  
  
 `piCurrentParameter`  
 弄包含当前位置的参数的索引。 如果当前位置位于函数名称上，则返回-1。  
  
 仅当 `dwListTypesRequested` 包含 SCRIPT_CMPL_PARAMLIST 时，才填充 `piCurrentParameter` 值。  
  
 `ppunk`  
 类型信息，以 `IProvideMultipleClassInfo` 对象的形式提供。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IProvideMultipleClassInfo 接口](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.iprovidemultipleclassinfo)   
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)