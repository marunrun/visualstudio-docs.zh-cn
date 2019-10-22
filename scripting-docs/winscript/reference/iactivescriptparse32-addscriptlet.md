---
title: IActiveScriptParse32：： AddScriptlet |Microsoft Docs
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
ms.openlocfilehash: b48d89ce2c49bd971fe298d2b4773aad8b65e8c3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72561692"
---
# <a name="iactivescriptparse32addscriptlet"></a>IActiveScriptParse32::AddScriptlet
向脚本中添加代码 scriptlet。 此方法用于以下环境：该脚本的持久状态与主机文档过度交织，而主机负责还原脚本，而不是通过 `IPersist*` 接口。 主要示例是 HTML 脚本语言，它们允许将嵌入在 HTML 文档中的代码 scriptlet 附加到内部事件（例如 ONCLICK = "button1 = ' Exit '"）。  
  
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
 中要与 scriptlet 关联的默认名称的地址。 如果 scriptlet 不包含命名信息（如上面的 ONCLICK 示例所示），则此名称将用于识别 scriptlet。 如果此参数 `NULL`，则脚本引擎将根据需要制造唯一名称。  
  
 `pstrCode`  
 中要添加的 scriptlet 文本的地址。 此字符串的解释取决于脚本语言。  
  
 `pstrItemName`  
 中包含与此 scriptlet 关联的项名称的缓冲区的地址。 除了 `pstrSubItemName` 之外，此参数还标识 scriptlet 为其事件处理程序的对象。  
  
 `pstrSubItemName`  
 中缓冲区的地址，其中包含与此 scriptlet 关联的已命名项的 `subobject` 名称;此名称必须在命名项的类型信息中找到。 如果 scriptlet 要与命名项而不是 `subitem` 相关联，则此参数为 NULL。 除了 `pstrItemName` 之外，此参数还标识 scriptlet 为其事件处理程序的特定对象。  
  
 `pstrEventName`  
 中缓冲区的地址，该缓冲区包含 scriptlet 为其事件处理程序的事件的名称。  
  
 `pstrDelimiter`  
 中Scriptlet 分隔符的地址。 从文本流分析 `pstrCode` 参数时，主机通常使用分隔符（如两个单引号（' '）来检测 scriptlet 的末尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记 scriptlet 的末尾，则将此参数设置为 NULL。  
  
 `dwSourceContextCookie`  
 中用于调试的应用程序定义的值。  
  
 `ulStartingLineNumber`  
 中从零开始的值，指定分析将从哪个行开始。  
  
 `dwFlags`  
 中与 scriptlet 关联的标志。 可以是以下值的组合：  
  
|返回值|含义|  
|------------------|-------------|  
|SCRIPTTEXT_ISVISIBLE|指示脚本文本应显示为脚本的命名空间中的全局方法（因此可按名称调用）。|  
|SCRIPTTEXT_ISPERSISTENT|指示如果保存脚本引擎（例如，通过调用 `IPersist*::Save`）或者通过转换回已初始化状态重置脚本引擎，则应保存在此调用过程中添加的代码。 有关此状态的详细信息，请参阅脚本引擎状态。|  
  
 `pbstrName` ,  
 弄用于标识 scriptlet 的实际名称。 这是按优先顺序排列的：在 scriptlet 文本中显式指定的名称、`pstrDefaultName` 中提供的默认名称或脚本引擎合成的唯一名称。  
  
 `pexcepinfo` ,  
 弄包含异常信息的结构的地址。 如果返回 DISP_E_EXCEPTION，则应填写此结构。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`DISP_E_EXCEPTION`|分析 scriptlet 时出现异常。 @No__t_0 参数包含有关异常的信息。|  
|`E_INVALIDARG`|参数无效。|  
|`E_NOTIMPL`|此方法不受支持;脚本引擎不支持添加事件-接收 scriptlet。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎尚未加载或初始化），因此失败。|  
|`OLESCRIPT_E_INVALIDNAME`|提供的默认名称在此脚本语言中无效。|  
|`OLESCRIPT_E_SYNTAX`|Scriptlet 中发生未指定的语法错误。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)