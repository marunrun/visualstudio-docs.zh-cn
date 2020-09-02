---
title: IDebugAddress |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb6344885e9e30c056982b15b8323eef3ef467b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165178"
---
# <a name="idebugaddress"></a>IDebugAddress
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示项的地址。 它由符号处理程序返回。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugAddress : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序实现此接口以表示对象的地址。  
  
## <a name="notes-for-callers"></a>调用方说明  
 许多接口上的许多方法都返回此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 此接口实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|检索描述对象及其位置的 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 结构。|  
  
## <a name="remarks"></a>备注  
 符号提供程序返回此接口以表示对象及其在特定范围 (例如，函数、方法或类) 中的位置。 此接口从返回并传递给符号提供程序和表达式计算器的各种方法。 通常，符号提供程序是唯一需要解释此接口内容的实体。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
