---
title: IActiveScriptParseProcedure32：:P arseProcedureText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ede37171-2f1e-4467-a358-17bd4a4f1869
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 713421a43d24d8ed7060b3ec4dfbf0f1c42e6249
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574885"
---
# <a name="iactivescriptparseprocedure32parseproceduretext"></a>IActiveScriptParseProcedure32：:P arseProcedureText
分析给定的代码过程，并将过程添加到命名空间。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseProcedureText(  
    LPCOLESTR pstrCode,              // address of procedure text  
    LPCOLESTR pstrFormalParams,      // address of formal parameter names  
    LPCOLESTR pstrProcedureName,     // address of procedure name  
    LPCOLESTR pstrItemName,          // address of item name  
    IUnknown *punkContext,           // address of debugging context  
    LPCOLESTR pstrDelimiter,         // address of end-of-procedure delimiter  
    DWORD_PTR dwSourceContextCookie, // application-defined value for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // procedure flags  
    IDispatch **ppdisp               // receives IDispatch pointer  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrCode`  
 中要计算的过程文本的地址。 此字符串的解释取决于脚本语言。  
  
 `pstrFormalParams`  
 中过程的正式参数名称的地址。 参数名称必须与脚本引擎的相应分隔符分隔开。 名称不应括在括号中。  
  
 `pstrProcedureName`  
 中要分析的过程名称的地址。  
  
 `pstrItemName`  
 中为要在其中计算过程的上下文提供的项名称的地址。 如果 `NULL` 此参数，则在脚本引擎的全局上下文中计算代码。  
  
 `punkContext`  
 中上下文对象的地址。 此对象保留供在调试环境中使用，调试器可能会提供此类上下文来表示活动的运行时上下文。 如果 `NULL` 此参数，则引擎将使用 `pstrItemName` 来标识上下文。  
  
 `pstrDelimiter`  
 中过程结束分隔符的地址。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测过程的结尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记过程的结束，则将此参数设置为 `NULL`。  
  
 `dwSourceContextCookie`  
 中用于调试的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 中从零开始的值，指定分析将从哪个行开始。  
  
 `dwFlags`  
 中与过程关联的标志。 可以是这些值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|指示 `pstrCode` 中的代码是表示过程的返回值的表达式。 默认情况下，代码可以包含表达式、语句列表或脚本语言在过程中允许的任何其他内容。|  
|SCRIPTPROC_IMPLICIT_THIS|指示 `this` 指针包含在过程的作用域中。|  
|SCRIPTPROC_IMPLICIT_PARENTS|指示 `this` 指针的父项包含在过程的作用域中。|  
  
 `ppdisp`  
 弄包含脚本的全局方法和属性的对象的指针地址。 如果脚本引擎不支持此类对象，则会返回 `NULL`。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持将过程的运行时添加到命名空间。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎处于未初始化或已关闭状态）。|  
|`OLESCRIPT_E_SYNTAX`|过程中出现未指定的语法错误。|  
|`S_FALSE`|脚本引擎不支持调度对象;`ppdisp` 参数设置为 `NULL`。|  
  
## <a name="remarks"></a>备注  
 此调用期间不计算任何脚本代码;相反，该过程编译为脚本状态，在此过程中，脚本可以在以后调用它。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParseProcedure32](../../winscript/reference/iactivescriptparseprocedure32.md)