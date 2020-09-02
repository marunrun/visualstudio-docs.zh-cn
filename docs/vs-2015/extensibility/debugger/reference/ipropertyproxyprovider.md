---
title: IPropertyProxyProvider |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700036"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供代理接口以查看和更改对象的数据。  
  
## <a name="syntax"></a>语法  
  
```  
IPropertyProxyProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器 (EE) 在实现 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) 接口的对象上实现此接口，该对象作为 EE 对类型可视化工具的支持的一部分。  
  
## <a name="notes-for-callers"></a>调用方说明  
 在接口上调用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) `IDebugProperty3` 以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 `IPropertyProxyProvider`接口实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|检索用于查看对象上数据的属性代理接口。|  
  
## <a name="remarks"></a>备注  
 尽管 EE 实现了此接口，但 [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) 的实现通常由 [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)进行处理。 有关获取 IEEVisualizerService 接口的详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)   
 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
