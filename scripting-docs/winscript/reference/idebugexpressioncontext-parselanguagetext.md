---
title: IDebugExpressionContext::ParseLanguageText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpressionContext.ParseLanguageText
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpressionContext::ParseLanguageText
ms.assetid: 650cb016-7d80-4011-b264-780f871a3466
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 50f9f398b9193c776f8e2a823b78ce7b8da438b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946272"
---
# <a name="idebugexpressioncontextparselanguagetext"></a>IDebugExpressionContext::ParseLanguageText
创建指定的文本的调试表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ParseLanguageText(  
   LPCOLESTR           pstrCode,  
   UINT                nRadix,  
   LPCOLESTR           pstrDelimiter,  
   DWORD               dwFlags,  
   IDebugExpression**  ppe  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrCode`  
 [in]提供的表达式或语句的文本。  
  
 `nRadix`  
 [in]若要使用的基数。  
  
 `pstrDelimiter`  
 [in]最终的脚本块分隔符。 当`pstrCode`进行分析的文本流，从主机通常使用分隔符，如两个单引号 （'），以检测脚本块的末尾。 此参数指定主机使用，允许脚本引擎来提供某些条件的原始预处理的分隔符 （例如，与使用用作分隔符的两个单引号替换单引号 [']）。 完全如何 （以及是否） 脚本的引擎使用此信息取决于脚本引擎。 将此参数设置为`NULL`如果主机不使用分隔符来标记的脚本块的结尾。  
  
 `dwFlags`  
 [in]以下的调试文本标志的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|DEBUG_TEXT_ISEXPRESSION|0x00000001|指示该文本是而不是语句表达式。 此标志可能会影响在其中的一些语言分析文本的方式。|  
|DEBUG_TEXT_RETURNVALUE|0x00000002|如果返回值不可用，调用方将使用它。|  
|DEBUG_TEXT_NOSIDEEFFECTS|0x00000004|不允许副作用。 如果设置此标志，该表达式的计算应更改任何运行时状态。|  
|DEBUG_TEXT_ALLOWBREAKPOINTS|0x00000008|允许文本求值时的断点。 如果未设置此标志的断点将会忽略文本求值时。|  
|DEBUG_TEXT_ALLOWERRORREPORT|0x00000010|允许文本求值时的错误报告。 如果未设置此标志然后错误不会报告到的主机在计算过程。|  
|DEBUG_TEXT_EVALUATETOCODECONTEXT|0x00000020|指示表达式的计算结果为代码上下文，而不是运行该表达式本身|  
  
 `ppe`  
 [out]返回指定的文本的调试表达式。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法创建指定的文本的调试表达式。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpressionContext 接口](../../winscript/reference/idebugexpressioncontext-interface.md)