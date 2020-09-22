---
title: IDebugSymbolSearchEvent2：： GetSymbolSearchInfo |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c8ef097ed02ae90b03289e3a2f3a1ad3f0ad8618
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840404"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

由事件处理程序调用以检索有关符号加载过程的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetSymbolSearchInfo(  
   IDebugModule3**    pModule,  
   BSTR*              pbstrDebugMessage,  
   MODULE_INFO_FLAGS* pdwModuleInfoFlags  
);  
```  
  
```csharp  
int GetSymbolSearchInfo(  
   IDebugModule3              pModule,   
   ref string                 pbstrDebugMessage,   
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags  
);  
  
```  
  
#### <a name="parameters"></a>parameters  
 `pModule`  
 弄一个 IDebugModule3 对象，表示要为其加载符号的模块。  
  
 `pbstrDebugMessage`  
 [in，out]返回一个字符串，其中包含来自模块的任何错误消息。 如果没有错误，则此字符串只包含模块的名称，但绝不会为空。  
  
> [!NOTE]
> [C + +] `pbstrDebugMessage` 不能为 `NULL` ，必须用来释放 `SysFreeString` 。  
  
 `pdwModuleInfoFlags`  
 弄 [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md) 枚举中的标志的组合，指示是否已加载任何符号。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 当尝试加载模块的调试符号后，处理程序收到 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) 事件后，处理程序可以调用 thismethod 来确定该负载的结果。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)   
 [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)   
 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
