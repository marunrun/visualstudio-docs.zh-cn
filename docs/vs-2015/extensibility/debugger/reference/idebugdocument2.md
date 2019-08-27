---
title: IDebugDocument2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2cd6afb417de4d8a362916f91593d0d0e67d307c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156502"
---
# <a name="idebugdocument2"></a>IDebugDocument2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示源文档。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDocument2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 通常可实现此接口。 它需要提供的源代码和磁盘上不存在源时，调试引擎 (DE) 还可以实现此接口。  在这种情况下，还将实现 DE [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)并[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)接口，以及一些其他方法[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)并[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 上的方法`IDebugDocumentContext2`， `IDebugDisassemblyStream2`， `IDebugDocumentPosition2`，和`IDebugActivateDocumentEvent2`接口返回此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugDocument2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|获取文档的名称中有几种形式之一。|  
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|获取文档的类标识符。|  
  
## <a name="remarks"></a>备注  
 仅当 DE 提供的源代码时，实现此接口。 例如，调试 HTML 页面上的脚本时，DE 提供的源代码由于下载或动态生成的源，并且不存在为磁盘文件。 当调试传统语言中，如C++，不需要实现此接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)   
 [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)   
 [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)   
 [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)   
 [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
