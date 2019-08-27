---
title: IActiveScriptParse::ParseScriptText | Microsoft Docs
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
ms.openlocfilehash: 3396aee8c044ee9b84d7d6256c6ad69a99965170
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954879"
---
# <a name="iactivescriptparseparsescripttext"></a>IActiveScriptParse::ParseScriptText
分析给定的代码 scriptlet，添加声明到命名空间和评估与相应的代码。  
  
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
|`pstrCode`|[in]要计算的 scriptlet 文本的地址。 此字符串的解释取决于脚本语言。|  
|`pstrItemName`|[in]项名称，是用要计算 scriptlet 的上下文的地址。 如果此参数为 NULL，脚本引擎的全局上下文中计算代码。|  
|`punkContext`|[in]上下文对象的地址。 此对象保留在调试环境，可能会由调试器来表示活动的运行时上下文中提供此类上下文中使用。 如果此参数为 NULL，则引擎使用`pstrItemName`来标识上下文。|  
|`pstrDelimiter`|[in]结束 scriptlet 分隔符的地址。 当`pstrCode`进行分析的文本流，从主机通常使用分隔符，如两个单引号 （'），检测 scriptlet 的末尾。 此参数指定主机使用，允许脚本引擎来提供某些条件的原始预处理的分隔符 （例如，与使用用作分隔符的两个单引号替换单引号 [']）。 完全如何 （以及是否） 引擎建立使用此信息取决于脚本引擎的脚本。 将此参数设置为`NULL`如果主机不使用分隔符来标记 scriptlet 的末尾。|  
|`dwSourceContextCookie`|[in]出于调试目的使用 cookie。|  
|`ulStartingLineNumber`|[in]指定分析开始的行的从零开始值。|  
|`dwFlags`|[in]与 scriptlet 相关联的标志。 可以是这些值的组合：|  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTEXT_ISEXPRESSION|如果计算表达式和语句之间的差异非常重要，但在脚本语言的语法模糊，此标志指定 scriptlet 会被解释为表达式，而不是语句或语句的列表。 默认情况下，除非可以从 scriptlet 文本的语法确定正确的选择，否则要假定语句。|  
|SCRIPTTEXT_ISPERSISTENT|指示是否保存脚本引擎应保存在此调用过程中添加的代码 (例如，通过调用`IPersist*::Save`)，或如果脚本引擎通过转换为初始化状态重置。|  
|SCRIPTTEXT_ISVISIBLE|指示脚本文本应显示 (并因此可按名称调用) 作为脚本的名称空间中的全局方法。|  
  
|||  
|-|-|  
|`pvarResult`|[out]接收 scriptlet 处理结果的缓冲区的地址或`NULL`如果调用方希望无结果 （即，不设置 SCRIPTTEXT_ISEXPRESSION 值）。|  
|`pexcepinfo`|[out]接收异常信息结构的地址。 如果填充此结构`IActiveScriptParse::ParseScriptText`返回 DISP_E_EXCEPTION。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`DISP_E_EXCEPTION`|在处理 scriptlet 中出现异常。 `pexcepinfo`参数包含有关异常的信息。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_NOTIMPL`|不支持此方法。 脚本引擎不支持运行时计算的表达式或语句。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎处于未初始化或已关闭状态，或已设置 SCRIPTTEXT_ISEXPRESSION 标志和脚本引擎处于初始化状态）。|  
|`OLESCRIPT_E_SYNTAX`|Scriptlet 中出现未指定的语法错误。|  
  
## <a name="remarks"></a>备注  
 如果脚本引擎处于初始化状态时，没有代码将实际在期间计算此调用;相反，此类代码是排队和执行时脚本引擎转换到 （或通过） 已启动的状态。 在初始化状态中不允许执行，因为它是错误调用此方法中初始化状态时的 SCRIPTTEXT_ISEXPRESSION 标志。  
  
 Scriptlet 可以是表达式、 语句的列表，或允许的脚本语言的任何内容。 例如，在 HTML 的评估中使用此方法\<脚本 > 标记，它允许语句执行，因为正在构造的 HTML 页，而不是仅将其编译成脚本状态。  
  
 传递给此方法的代码必须是有效的完整部分代码。 例如，在 VBScript 中是非法的调用与子进行一次此方法，然后使用第二次`End Sub`。 分析器必须等待完成子例程，第二次调用，但因为子例程声明已启动但尚未完成，而不是就必须生成分析错误。  
  
 有关脚本状态的详细信息，请参阅脚本引擎状态章节[Windows 脚本引擎](../../winscript/windows-script-engines.md)。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)