---
title: IActiveScriptAuthor::GetInfoFromContext | Microsoft Docs
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
ms.openlocfilehash: e4fe885e116019608dd8d748c3cbdaff5d31dd2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935381"
---
# <a name="iactivescriptauthorgetinfofromcontext"></a>IActiveScriptAuthor::GetInfoFromContext
返回类型的代码块中的信息和给定的字符的定位点位置。 IntelliSense、 全局列表和参数的提示，这提供有关成员的信息。  
  
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
 [in]用于生成的信息结果的代码块字符串的地址。  
  
 `cchCode`  
 [in]代码块的长度。  
  
 `ichCurrentPosition`  
 [in]该字符的位置相对于开始块。  
  
 `dwListTypesRequested`  
 [in]请求列表类型。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_NOLIST|0x0000|没有列表。|  
|SCRIPT_CMPL_MEMBERLIST|0x0001|成员的列表。|  
|SCRIPT_CMPL_ENUMLIST|0x0002|枚举列表。|  
|SCRIPT_CMPL_PARAMLIST|0x0004|调用方法参数列表。|  
|SCRIPT_CMPL_GLOBALLIST|0x0008|全局列表。|  
  
 SCRIPT_CMPL_GLOBALLIST 类型会被视为可以与其他完成项使用 OR 运算符组合的默认值完成项。 脚本首先创作引擎会尝试填充其他的完成列表项的类型信息。 如果失败，则引擎会为 SCRIPT_CMPL_GLOBALLIST 填充。  
  
 `pdwListTypesProvided`  
 [out]提供的列表的类型。  
  
 `pichListAnchorPosition`  
 [out]上下文包含当前的位置的起始索引。 起始索引是相对于块的开始。  
  
 填充此值时，才`dwListTypesRequested`包括 SCRIPT_CMPL_MEMBERLIST、 SCRIPT_CMPL_ENUMLIST 或 SCRIPT_CMPL_GLOBALLIST。 对于其他请求的列表类型，则结果不可确定。  
  
 `pichFuncAnchorPosition`  
 [out]函数调用，其中包含当前的位置的起始索引。 起始索引是相对于块的开始。  
  
 仅当上下文包含当前的位置是函数调用，以及时填充此`dwListTypesRequested`包括 SCRIPT_CMPL_PARAMLIST。 否则，结果是不确定的。  
  
 `pmemid`  
 [out]某个类型中定义的函数的 MEMBERID `IProvideMultipleClassInfo``ppunk` out 参数。  
  
 填充此值时，才`dwListTypesRequested`包括 SCRIPT_CMPL_PARAMLIST。  
  
 `piCurrentParameter`  
 [out]包含当前的位置的参数的索引。 如果当前位置位于函数名称，则返回-1。  
  
 `piCurrentParameter`填充值时，才`dwListTypesRequested`包括 SCRIPT_CMPL_PARAMLIST。  
  
 `ppunk`  
 中的窗体提供的类型信息`IProvideMultipleClassInfo`对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IProvideMultipleClassInfo 接口](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.iprovidemultipleclassinfo)   
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)