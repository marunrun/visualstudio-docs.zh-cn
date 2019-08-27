---
title: IActiveScriptParse32::AddScriptlet | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fcf11eb2-8e71-4cca-afda-a91791c243ff
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: b5a680eea5f5695d3a7253b9cf722af6ebf537c6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954878"
---
# <a name="iactivescriptparse32addscriptlet"></a>IActiveScriptParse32::AddScriptlet
将代码 scriptlet 添加到该脚本。 此方法使用环境中使用主机文档混合在一起的持久状态的脚本主机负责还原脚本，而不通过`IPersist*`接口。 主要示例是允许要附加到内部事件的 HTML 文档中嵌入的代码 scriptlet 的 HTML 脚本语言 (例如，ONCLICK="button1.text='Exit")。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddScriptlet(  
    LPCOLESTR pstrDefaultName,       // address of default name of scriptlet  
    LPCOLESTR pstrCode,              // address of scriptlet text  
    LPCOLESTR pstrItemName,          // address of item name  
    LPCOLESTR pstrSubItemName,       // address of subitem name  
    LPCOLESTR pstrEventName,         // address of event name  
    LPCOLESTR pstrDelimiter,         // address of end-of-scriptlet delimiter  
    DWORD_PTR dwSourceContextCookie, // application-defined value for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // scriptlet flags  
    BSTR *pbstrName,                 // address of actual name of scriptlet  
    EXCEPINFO *pexcepinfo            // address of exception information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrDefaultName`  
 [in]若要将与 scriptlet 相关联的默认名称的地址。 如果 scriptlet 不包含命名信息 （如上面的 ONCLICK 示例），此名称将用于标识 scriptlet。 如果此参数为`NULL`，脚本引擎生成的唯一名称，如有必要。  
  
 `pstrCode`  
 [in]要添加的 scriptlet 文本的地址。 此字符串的解释取决于脚本语言。  
  
 `pstrItemName`  
 [in]包含与此 scriptlet 相关联的项名称的缓冲区的地址。 此参数，除了`pstrSubItemName`，标识 scriptlet 为事件处理程序的对象。  
  
 `pstrSubItemName`  
 [in]包含的名称的缓冲区的地址`subobject`与此 scriptlet 相关联; 必须在命名的项的类型信息中找到此名称的命名项。 此参数为 NULL，如果要与命名项而不是关联 scriptlet `subitem`。 此参数，除了`pstrItemName`，标识 scriptlet 为事件处理程序的特定对象。  
  
 `pstrEventName`  
 [in]包含为其 scriptlet 是一个事件处理程序的事件名称的缓冲区的地址。  
  
 `pstrDelimiter`  
 [in]结束 scriptlet 分隔符的地址。 当`pstrCode`参数分析从文本流，主机通常使用分隔符，如两个单引号 （'），检测 scriptlet 的末尾。 此参数指定主机使用，允许脚本引擎来提供某些条件的原始预处理的分隔符 （例如，与使用用作分隔符的两个单引号替换单引号 [']）。 完全如何 （以及是否） 引擎建立使用此信息取决于脚本引擎的脚本。 如果主机不使用分隔符来标记 scriptlet 的末尾，此参数设置为 NULL。  
  
 `dwSourceContextCookie`  
 [in]用于调试目的的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 [in]指定分析开始的行的从零开始值。  
  
 `dwFlags`  
 [in]与 scriptlet 相关联的标志。 可以是以下值的组合：  
  
|返回值|含义|  
|------------------|-------------|  
|SCRIPTTEXT_ISVISIBLE|指示脚本文本应显示 (并因此可按名称调用) 作为脚本的名称空间中的全局方法。|  
|SCRIPTTEXT_ISPERSISTENT|指示是否保存脚本引擎应保存在此调用过程中添加的代码 (例如，通过调用`IPersist*::Save`)，或如果脚本引擎通过转换为初始化状态重置。 有关此状态的详细信息，请参阅脚本引擎状态。|  
  
 `pbstrName` ,  
 [out]用来标识 scriptlet 的实际名称。 这是为了按优先顺序是： scriptlet 文本中显式指定一个名称，在提供的默认名称`pstrDefaultName`，或通过脚本引擎合成的唯一名称。  
  
 `pexcepinfo` ,  
 [out]一个包含异常信息结构的地址。 如果返回 DISP_E_EXCEPTION，应填充此结构。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`DISP_E_EXCEPTION`|Scriptlet 的分析中发生了异常。 `pexcepinfo`参数包含有关异常的信息。|  
|`E_INVALIDARG`|参数无效。|  
|`E_NOTIMPL`|不支持此方法;脚本引擎不支持添加事件接收 scriptlet。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化），因此失败。|  
|`OLESCRIPT_E_INVALIDNAME`|提供的默认名称是在此脚本语言中无效。|  
|`OLESCRIPT_E_SYNTAX`|Scriptlet 中出现未指定的语法错误。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)