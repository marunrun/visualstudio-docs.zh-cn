---
title: IDebugClassField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2bd5dfaea68abae6730a97efdff088ca6e7c7a00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696988"
---
# <a name="idebugclassfield"></a>IDebugClassField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口将类表示为类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugClassField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序在实现 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口的同一对象上实现此接口。 此接口是表示类类型的专用化。  
  
## <a name="notes-for-callers"></a>调用方说明  
 许多接口具有可返回此接口的方法，包括 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)和 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)。 此外，如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法返回标志，则可以使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口 `FIELD_TYPE_CLASS` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 和 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口上的方法，此接口还实现以下内容：  
  
|方法|说明|  
|------------|-----------------|  
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|为此类的基类创建一个枚举器。|  
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|确定是否在类中定义了特定接口。|  
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|为此类的嵌套类创建枚举数。|  
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|获取包含此类的类。|  
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|为此类实现的接口创建一个枚举器。|  
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|为此类的构造函数创建一个枚举器。|  
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|获取默认索引器的名称。|  
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|创建此类的嵌套枚举器的枚举数。|  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
