---
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c1f30c3a465d4803e5c91f14ee45ad582e76d986
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200215"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示源文件中作为字符偏移量的位置。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDocumentPositionOffset2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 通过 IDE 实现和使用的调试引擎。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugDocumentPositionOffset2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|检索当前的文档位置的范围。|  
  
## <a name="remarks"></a>备注  
 这将返回相同的信息[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)但在`char`从文档开头的偏移量。 这提供了文档，它将存在磁盘上，它是字符，而不是通常返回的行和列信息的一维数组。  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
