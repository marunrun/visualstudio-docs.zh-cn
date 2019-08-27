---
title: IDebugDocumentPosition2::GetRange |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 189810280bd5db4573ba45c2335b8bb96a163abb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200261"
---
# <a name="idebugdocumentposition2getrange"></a>IDebugDocumentPosition2::GetRange
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取此文档位置的范围。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetRange(   
   TEXT_POSITION* pBegPosition,  
   TEXT_POSITION* pEndPosition  
);  
```  
  
```csharp  
int GetRange(   
   TEXT_POSITION[] pBegPosition,  
   TEXT_POSITION[] pEndPosition  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pBegPosition`  
 [in、 out]一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)填充的起始位置的结构。 如果不需要此信息，请将此参数设置为 null 值。  
  
 `pEndPosition`  
 [in、 out]一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)填充的结束位置的结构。 如果不需要此信息，请将此参数设置为 null 值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 在一个位置断点的文档位置中指定的范围是调试引擎 (DE) 用于实际影响代码的语句继续搜索。 例如，考虑以下代码：  
  
```  
Line 5: // comment  
Line 6: x = 1;  
```  
  
 第 5 行分配到正在调试的程序的任何代码。 如果行 5 设置断点调试器想 DE 向前搜索一定影响代码的第一行，调试器会指定一系列，包括其他候选行断点可能会正确放。 DE 将然后向前搜索这些行直到找到可接受断点的行。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
