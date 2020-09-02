---
title: IEEDataStorage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad398380c7c951b99e7d84283355ee9d31955173
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704735"
---
# <a name="ieedatastorage"></a>IEEDataStorage
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示字节数组。  
  
## <a name="syntax"></a>语法  
  
```  
IEEDataStorage : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器 (EE) 实现此接口，以表示由类型可视化工具使用的字节数组 (通过 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 接口) 来检索和更改数据。 EE 通常实现此接口以支持外部类型可视化工具。  
  
## <a name="notes-for-callers"></a>调用方说明  
 接口上的方法 `IPropertyProxyEESide` 都返回此接口。 调用 [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) 以获取 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 接口。 在[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口上调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)以获取[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 `IEEDataStorage`接口实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|检索指定数目的数据字节到提供的缓冲区。|  
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|检索可用的数据字节数。|  
  
## <a name="remarks"></a>备注  
 此接口由类型可视化工具用来访问由特定对象保存的数据。 数据被视为字节数组，使类型可视化工具能够以向用户显示它所需的任何方式对其进行操作。  
  
 如果需要，自定义查看器还可以使用此接口，尽管更常见的情况是，自定义查看器会将自定义界面、 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) 或 [GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (用于面向字符串的数据) 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
