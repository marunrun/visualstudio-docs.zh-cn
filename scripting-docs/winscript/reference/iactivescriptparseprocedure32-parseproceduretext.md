---
title: IActiveScriptParseProcedure32::ParseProcedureText | Microsoft Docs
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
ms.openlocfilehash: e772d8276de5528f0aed25278a03725d09edb180
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993392"
---
# <a name="iactivescriptparseprocedure32parseproceduretext"></a>IActiveScriptParseProcedure32::ParseProcedureText
分析给定的代码过程并将该过程添加到命名空间。  
  
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
 [in]要评估的过程文本的地址。 此字符串的解释取决于脚本语言。  
  
 `pstrFormalParams`  
 [in]该过程的正式参数名称的地址。 参数名称必须与脚本引擎的适当分隔符分隔。 名称不应括在括号中。  
  
 `pstrProcedureName`  
 [in]要分析的过程名称的地址。  
  
 `pstrItemName`  
 [in]提供该过程将在其中计算的上下文的项目名称的地址。 如果此参数为`NULL`，脚本引擎的全局上下文中计算代码。  
  
 `punkContext`  
 [in]上下文对象的地址。 此对象保留在调试环境，可能会由调试器来表示活动的运行时上下文中提供此类上下文中使用。 如果此参数为`NULL`，该引擎使用`pstrItemName`来标识上下文。  
  
 `pstrDelimiter`  
 [in]过程结束分隔符的地址。 当`pstrCode`进行分析的文本流，从主机通常使用分隔符，如两个单引号 （'），来检测该过程结束。 此参数指定主机使用，允许脚本引擎来提供某些条件的原始预处理的分隔符 （例如，与使用用作分隔符的两个单引号替换单引号 [']）。 完全如何 （以及是否） 引擎建立使用此信息取决于脚本引擎的脚本。 将此参数设置为`NULL`如果主机不使用分隔符来标记该过程的结尾。  
  
 `dwSourceContextCookie`  
 [in]用于调试目的的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 [in]指定分析开始的行的从零开始值。  
  
 `dwFlags`  
 [in]与该过程关联的标志。 可以是这些值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|指示中的代码`pstrCode`一个表达式，表示该过程的返回值。 默认情况下，代码可以包含表达式、 语句的列表，或任何其他过程中允许的脚本语言。|  
|SCRIPTPROC_IMPLICIT_THIS|指示`this`指针包括在该过程的范围。|  
|SCRIPTPROC_IMPLICIT_PARENTS|指示的父级`this`指针包括在该过程的范围。|  
  
 `ppdisp`  
 [out]包含脚本的全局方法和属性的对象的指针的地址。 如果脚本引擎不支持此类对象，`NULL`返回。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持运行时添加到命名空间的过程。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎处于未初始化或已关闭状态）。|  
|`OLESCRIPT_E_SYNTAX`|在过程中出现未指定的语法错误。|  
|`S_FALSE`|脚本引擎不支持的调度对象;`ppdisp`参数设置为`NULL`。|  
  
## <a name="remarks"></a>备注  
 在此调用; 期间不计算任何脚本代码相反，该过程被编译成脚本状态，它可以由调用脚本更高版本。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParseProcedure32](../../winscript/reference/iactivescriptparseprocedure32.md)