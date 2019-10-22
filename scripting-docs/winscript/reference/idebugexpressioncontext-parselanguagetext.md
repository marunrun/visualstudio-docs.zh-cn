---
title: IDebugExpressionContext：:P arseLanguageText |Microsoft Docs
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
ms.openlocfilehash: 0493adde76e029088b637be3c6aaf02c55caaace
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573153"
---
# <a name="idebugexpressioncontextparselanguagetext"></a>IDebugExpressionContext::ParseLanguageText
为指定的文本创建一个调试表达式。  
  
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
 中提供表达式或语句的文本。  
  
 `nRadix`  
 中要使用的基数。  
  
 `pstrDelimiter`  
 中脚本结束分隔符。 当从文本流分析 `pstrCode` 时，主机通常使用分隔符（如两个单引号（' '）来检测脚本块的结尾。 此参数指定主机使用的分隔符，允许脚本引擎提供某些条件基元预处理（例如，用两个单引号替换单引号 ['] 以用作分隔符）。 脚本引擎使用此信息的确切方式取决于脚本引擎。 如果主机未使用分隔符来标记脚本块的末尾，则将此参数设置为 `NULL`。  
  
 `dwFlags`  
 中以下调试文本标志的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|DEBUG_TEXT_ISEXPRESSION|0x00000001|指示文本是一个表达式，而不是语句。 此标志可能会影响某些语言分析文本的方式。|  
|DEBUG_TEXT_RETURNVALUE|0x00000002|如果返回值可用，则调用方将使用该返回值。|  
|DEBUG_TEXT_NOSIDEEFFECTS|0x00000004|不允许副作用。 如果设置了此标志，则表达式的计算应更改为 "无运行时状态"。|  
|DEBUG_TEXT_ALLOWBREAKPOINTS|0x00000008|允许在文本计算期间发生断点。 如果未设置此标志，则在对文本进行计算的过程中将忽略断点。|  
|DEBUG_TEXT_ALLOWERRORREPORT|0x00000010|允许在对文本进行计算的过程中报告错误。 如果未设置此标志，则在评估过程中不对主机报告错误。|  
|DEBUG_TEXT_EVALUATETOCODECONTEXT|0x00000020|指示表达式将计算为代码上下文而不是运行表达式本身|  
  
 `ppe`  
 弄返回指定文本的调试表达式。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法为指定的文本创建一个调试表达式。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpressionContext 接口](../../winscript/reference/idebugexpressioncontext-interface.md)