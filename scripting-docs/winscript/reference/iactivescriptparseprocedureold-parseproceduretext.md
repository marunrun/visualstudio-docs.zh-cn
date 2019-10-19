---
title: IActiveScriptParseProcedureOld：:P arseProcedureText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld.ParseProcedureText
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld::ParseProcedureText
ms.assetid: 21a21313-35ce-432d-b9a6-7999065f19ac
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 116cbc7fac0d53b55c9766945d56ecebd27b6785
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577453"
---
# <a name="iactivescriptparseprocedureoldparseproceduretext"></a>IActiveScriptParseProcedureOld::ParseProcedureText
分析给定的代码过程，并将匿名过程添加到命名空间。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseProcedureText(  
   LPCOLESTR    pstrCode,  
   LPCOLESTR    pstrFormalParams,  
   LPCOLESTR    pstrItemName,  
   IUnknown*    punkContext,  
   LPCOLESTR    pstrDelimiter,  
   DWORD_PTR    dwSourceContextCookie,  
   ULONG        ulStartingLineNumber,  
   DWORD        dwFlags,  
   IDispatch**  ppdisp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrCode`  
 中要计算的过程文本。 此字符串的解释取决于脚本语言。  
  
 `pstrFormalParams`  
 中过程的形参名称。 参数名称必须与脚本引擎的相应分隔符分隔开。 名称不应括在括号中。  
  
 `pstrItemName`  
 中命名项的名称，该名称提供要在其中计算过程的上下文。 如果 `NULL` 此参数，则在脚本引擎的全局上下文中计算代码。  
  
 `punkContext`  
 中上下文对象。 此对象保留供在调试环境中使用，调试器可能会提供此类上下文来表示活动的运行时上下文。 如果 `NULL` 此参数，则引擎将使用 `pstrItemName` 来标识上下文。  
  
 `pstrDelimiter`  
 中过程末尾分隔符。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测过程的结尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记过程的结束，则将此参数设置为 `NULL`。  
  
 `dwSourceContextCookie`  
 中用于调试的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 中从零开始的值，指定分析将开始的行。  
  
 `dwFlags`  
 中与过程关联的标志。 可以是这些值的组合。  
  
|返回的常量|“值”|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|0x00000020|指示 `pstrCode` 中的代码是表示过程的返回值的表达式。|  
|SCRIPTPROC_IMPLICIT_THIS|0x00000100|指示 `this` 指针包含在过程的作用域中。|  
|SCRIPTPROC_IMPLICIT_PARENTS|0x00000200|指示 `this` 指针的父项包含在过程的作用域中。|  
  
 `ppdisp`  
 弄返回一个调度包装，其中默认方法是此方法分析的过程。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持将过程的运行时添加到命名空间。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎处于未初始化或已关闭状态）。|  
|`OLESCRIPT_E_SYNTAX`|过程中出现未指定的语法错误。|  
|`S_FALSE`|脚本引擎不支持调度对象;`ppdisp`parameter 设置为 `NULL`。|  
  
## <a name="remarks"></a>备注  
 此调用期间不计算任何脚本代码;相反，该过程编译到 `ppdisp` 的方法中，稍后脚本可以在该方法中调用它。  
  
 此接口已弃用，以支持 `IActiveScriptParseProcedure` 接口。 @No__t_0 方法类似于此方法，但允许指定过程名称。 在所有情况下，都应使用 `IActiveScriptParseProcedure::ParseProcedureText`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParseProcedureOld 接口](../../winscript/reference/iactivescriptparseprocedureold-interface.md)   
 [IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)