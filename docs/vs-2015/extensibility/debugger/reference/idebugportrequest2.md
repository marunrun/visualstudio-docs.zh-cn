---
title: IDebugPortRequest2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa72ae9d2cfbe399c3507406875e9c692d18b678
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188342"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口描述一个端口。 此描述用于将端口添加到端口提供程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortRequest2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 Visual Studio 通常实现此接口从端口提供程序获取调试端口的过程中。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口传递到[端口](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)创建调试端口。 调用[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)返回此接口，表示用于第一个位置中创建该端口的请求。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugPortRequest2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|获取要创建的端口的名称。|  
  
## <a name="remarks"></a>备注  
 通常，调试引擎不与端口提供程序交互，并不会使用此接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)   
 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
