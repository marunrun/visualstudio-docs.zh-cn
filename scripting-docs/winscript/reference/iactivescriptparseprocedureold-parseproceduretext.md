---
title: IActiveScriptParseProcedureOld::ParseProcedureText | Microsoft Docs
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
ms.openlocfilehash: 8e521bbdcd8d7397c1c2dfb377fd9b41811499f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993210"
---
# <a name="iactivescriptparseprocedureoldparseproceduretext"></a>IActiveScriptParseProcedureOld::ParseProcedureText
分析给定的代码过程并将匿名过程添加到命名空间。  
  
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
 [in]要评估的过程文本。 此字符串的解释取决于脚本语言。  
  
 `pstrFormalParams`  
 [in]该过程的正式参数名称。 参数名称必须与脚本引擎的适当分隔符分隔。 名称不应括在括号中。  
  
 `pstrItemName`  
 [in]提供该过程将在其中计算的上下文的命名项的名称。 如果此参数为`NULL`，脚本引擎的全局上下文中计算代码。  
  
 `punkContext`  
 [in]上下文对象中。 此对象保留在调试环境，可能会由调试器来表示活动的运行时上下文中提供此类上下文中使用。 如果此参数为`NULL`，该引擎使用`pstrItemName`来标识上下文。  
  
 `pstrDelimiter`  
 [in]过程结束分隔符。 当`pstrCode`进行分析的文本流，从主机通常使用分隔符，如两个单引号 （'），来检测该过程结束。 此参数指定主机使用，允许脚本引擎来提供某些条件的分隔符 （例如，使用用作分隔符的两个单引号替换单引号 [']） 的原始预处理。 完全如何 （以及是否） 脚本的引擎使用此信息取决于脚本引擎。 将此参数设置为`NULL`如果主机不使用分隔符来标记该过程的结尾。  
  
 `dwSourceContextCookie`  
 [in]用于调试目的的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 [in]从零开始的值，指定在哪一行分析将开始。  
  
 `dwFlags`  
 [in]与该过程关联的标志。 可以是这些值的组合。  
  
|返回的常量|“值”|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|0x00000020|指示中的代码`pstrCode`一个表达式，表示该过程的返回值。|  
|SCRIPTPROC_IMPLICIT_THIS|0x00000100|指示`this`指针包括在该过程的范围。|  
|SCRIPTPROC_IMPLICIT_PARENTS|0x00000200|指示的父级`this`指针包括在该过程的范围。|  
  
 `ppdisp`  
 [out]返回一个调度包装器位置的默认方法是通过此方法分析的过程。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持运行时添加到命名空间的过程。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎处于未初始化或已关闭状态）。|  
|`OLESCRIPT_E_SYNTAX`|在过程中出现未指定的语法错误。|  
|`S_FALSE`|脚本引擎不支持的调度对象;`ppdisp`参数设置为`NULL`。|  
  
## <a name="remarks"></a>备注  
 在此调用; 期间不计算任何脚本代码相反，该过程编译到方法上`ppdisp`，它可以由调用脚本更高版本。  
  
 此接口已弃用的`IActiveScriptParseProcedure`接口。 `IActiveScriptParseProcedure::ParseProcedureText`方法类似于这种方法，但它允许指定的过程名称。 在所有情况下，`IActiveScriptParseProcedure::ParseProcedureText`应使用。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParseProcedureOld 接口](../../winscript/reference/iactivescriptparseprocedureold-interface.md)   
 [IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)