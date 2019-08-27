---
title: IPropertyProxyProvider | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39cdc7769765a7680905fca5faa49222bf0a3b6d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700036"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供了一个代理界面，用于查看和更改对象的数据。  
  
## <a name="syntax"></a>语法  
  
```  
IPropertyProxyProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器 (EE) 实现此接口上实现的相同对象[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口作为 EE 的支持的类型可视化工具的一部分。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上`IDebugProperty3`接口，以获得此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 `IPropertyProxyProvider`接口实现了以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|检索属性代理接口的对象上查看数据。|  
  
## <a name="remarks"></a>备注  
 尽管 EE 实现此接口的实现[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)通常由处理[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)。 请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)有关获取 IEEVisualizerService 接口的详细信息。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)   
 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
