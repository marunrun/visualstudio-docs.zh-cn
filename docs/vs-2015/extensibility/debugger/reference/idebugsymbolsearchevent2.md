---
title: IDebugSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fe6eda784ddfa393ee123a7aab1498fc2e5a15b5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694613"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口由调试引擎 (DE) 发送，以指示已加载的模块正在调试的调试符号。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSymbolSearchEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 DE 实现此接口以报告已加载模块的符号。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问`IDebugEvent2`接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 DE 创建并发送此事件对象来报告已加载模块的符号。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 `IDebugSymbolSearchEvent2`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|检索有关搜索结果的符号信息。|  
  
## <a name="remarks"></a>备注  
 将发送此事件，即使符号无法加载。 调用`IDebugSymbolSearchEvent2::GetSymbolSearchInfo`允许此事件以确定模块是否实际上有任何符号的处理程序。  
  
 Visual Studio 通常使用此事件来更新中加载符号的状态**模块**窗口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
