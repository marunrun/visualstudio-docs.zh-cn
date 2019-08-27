---
title: IDebugSettingsCallback2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c3e962c00d6c9230cab765ed56e7607cbfd91765
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153147"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

启用调试引擎读取指标设置远程。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSettingsCallback2D : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 此接口是由会话调试管理器的事件回调实现和使用的调试引擎。 它可能还用于本地而不是 Dbgmetric [d].lib。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugSettingsCallback2`。  
  
|方法|描述|  
|------------|-----------------|  
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|枚举给定语言和供应商标识符可用表达式计算器。|  
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|检索给定度量值的表达式计算器本地对象。|  
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|检索一个值，对应于指定的表达式计算器指标。|  
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|检索给定的名称或该度量值的表达式计算器指标文件。|  
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|检索在给定其名称的表达式计算器指标的唯一标识符。|  
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|检索在给定名称的表达式计算器指标的值字符串。|  
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|检索在给定名称的指标的值。|  
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|检索在给定名称的一个指标的唯一标识符。|  
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|检索在给定名称的度量值的值字符串。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 下面的示例演示采用的函数**IDebugSettingsCallback2**对象作为参数。  
  
```cpp#  
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)  
{  
    HRESULT hRes = E_FAIL;  
  
    if ( ppCallback )  
   {  
        if ( EVAL(m_pdec) )  
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);  
        else  
            hRes = E_FAIL;  
    }  
    else  
        hRes = E_INVALIDARG;  
  
    return ( hRes );  
}  
```
