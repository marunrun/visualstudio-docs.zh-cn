---
title: IActiveScriptParse：:P arseScriptText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParse.ParseScriptText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParse_ParseScriptText
ms.assetid: 2d237d6c-cc65-415b-8808-72791304a136
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b4f35b398a7348f4e2bdbaaa9ab3e322bf69ddb6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72561620"
---
# <a name="iactivescriptparseparsescripttext"></a>IActiveScriptParse::ParseScriptText
分析给定的代码 scriptlet，将声明添加到命名空间中，并根据需要对代码进行评估。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseScriptText(  
    LPCOLESTR pstrCode,              // address of scriptlet text  
    LPCOLESTR pstrItemName,          // address of item name  
    IUnknown *punkContext,           // address of debugging context  
    LPCOLESTR pstrDelimiter,         // address of end-of-scriptlet delimiter  
    DWORD_PTR dwSourceContextCookie, // cookie for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // scriptlet flags  
    VARIANT *pvarResult,             // address of buffer for results  
    EXCEPINFO *pexcepinfo            // address of buffer for error data  
);  
```  
  
#### <a name="parameters"></a>参数  
  
|||  
|-|-|  
|`pstrCode`|中要计算的 scriptlet 文本的地址。 此字符串的解释取决于脚本语言。|  
|`pstrItemName`|中为在其中计算 scriptlet 的上下文提供的项名称的地址。 如果此参数为 NULL，则在脚本引擎的全局上下文中计算代码。|  
|`punkContext`|中上下文对象的地址。 此对象保留供在调试环境中使用，调试器可能会提供此类上下文来表示活动的运行时上下文。 如果此参数为 NULL，则引擎将使用 `pstrItemName` 来标识上下文。|  
|`pstrDelimiter`|中Scriptlet 分隔符的地址。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测 scriptlet 的末尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记 scriptlet 的末尾，则将此参数设置为 `NULL`。|  
|`dwSourceContextCookie`|中用于调试的 Cookie。|  
|`ulStartingLineNumber`|中从零开始的值，指定分析将从哪个行开始。|  
|`dwFlags`|中与 scriptlet 关联的标志。 可以是这些值的组合：|  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTEXT_ISEXPRESSION|如果计算表达式和语句之间的差异很重要，但脚本语言中的语法不明确，则此标志指定 scriptlet 将解释为表达式，而不是声明为语句或语句列表。 默认情况下，将假定语句，除非可以通过 scriptlet 文本的语法来确定正确的选择。|  
|SCRIPTTEXT_ISPERSISTENT|指示如果保存脚本引擎（例如，通过调用 `IPersist*::Save`）或者通过转换回已初始化状态重置脚本引擎，则应保存在此调用过程中添加的代码。|  
|SCRIPTTEXT_ISVISIBLE|指示脚本文本应显示为脚本的命名空间中的全局方法（因此可按名称调用）。|  
  
|||  
|-|-|  
|`pvarResult`|弄接收 scriptlet 处理结果的缓冲区的地址，如果调用方不需要任何结果，则为 `NULL` （也就是说，未设置 SCRIPTTEXT_ISEXPRESSION 值）。|  
|`pexcepinfo`|弄接收异常信息的结构的地址。 如果 `IActiveScriptParse::ParseScriptText` 返回 DISP_E_EXCEPTION，则填充此结构。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`DISP_E_EXCEPTION`|处理 scriptlet 时出现异常。 @No__t_0 参数包含有关异常的信息。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持表达式或语句的运行时计算。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎处于未初始化或已关闭状态，或设置了 SCRIPTTEXT_ISEXPRESSION 标志，并且脚本引擎处于已初始化状态）。|  
|`OLESCRIPT_E_SYNTAX`|Scriptlet 中发生未指定的语法错误。|  
  
## <a name="remarks"></a>备注  
 如果脚本引擎处于已初始化状态，则在此调用期间将不会实际计算任何代码;相反，此类代码将排队并在脚本引擎转换为 "已启动" 状态时执行。 由于在初始化状态中不允许执行，因此当处于已初始化状态时，使用 SCRIPTTEXT_ISEXPRESSION 标志调用此方法是错误的。  
  
 Scriptlet 可以是表达式、语句列表或脚本语言允许的任何内容。 例如，此方法用于计算 HTML \<SCRIPT > 标记，这允许在构造 HTML 页时执行语句，而不只是将它们编译为脚本状态。  
  
 传递给此方法的代码必须是有效的完整代码部分。 例如，在 VBScript 中，使用 Sub 函数（x）调用此方法一次，然后使用 `End Sub` 进行第二次调用是非法的。 分析器不得等待第二次调用来完成子例程，而应生成分析错误，因为子程序声明已启动但未完成。  
  
 有关脚本状态的详细信息，请参阅[Windows 脚本引擎](../../winscript/windows-script-engines.md)的脚本引擎状态部分。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)