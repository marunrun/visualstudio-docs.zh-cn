---
title: IDebugDefaultPort2 | Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697519"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供用于访问端口的服务器和通知功能的几种方法。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDefaultPort2 : IDebugPort2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 Visual Studio 实现此接口来表示用于访问程序的调试端口。 如果处理远程调试，则，自定义端口提供程序还可以实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 上的方法的参数[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)接口提供此接口。 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口还可以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了中定义的方法[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|通过此端口获取端口通知接口。|  
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|获取承载此端口的服务器的接口。|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|确定此端口是否正在本地计算机上运行。|  
  
## <a name="remarks"></a>备注  
 名称"`IDebugDefaultPort2`"有点用词不当，因为它不表示默认端口。 无法调用"IDebugPort3。"  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
