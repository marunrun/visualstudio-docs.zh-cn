---
title: IDebugDefaultPort2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ca0b6b7e9753b346b8a995ffd8ddcb6cc53fe7c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697519"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供多种方法来访问端口的服务器和通知工具。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDefaultPort2 : IDebugPort2  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 Visual Studio 实现此接口，以表示用于访问程序的调试端口。 如果自定义端口供应商处理远程调试，还可以实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)接口上的方法的参数提供此接口。 在[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口上调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)还可以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 除了在 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)中定义的方法，此接口还实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|从此端口获取端口通知接口。|  
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|获取承载此端口的服务器的接口。|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|确定此端口是否在本地计算机上运行。|  
  
## <a name="remarks"></a>备注  
 名称 " `IDebugDefaultPort2` " 是 misnomer 的一个小数位，因为它不表示默认端口。 它可以名为 "IDebugPort3"。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
