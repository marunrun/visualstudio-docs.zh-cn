---
title: IDebugDynamicField | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 41cf0e397834f337863baa46abb4e6bbccee98ad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198512"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示变量的类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDynamicField : IDebugField  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序实现此接口作为基类的任何类型，可以在运行时确定。 这是仅用于托管代码。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口表示可从中派生更专业的接口的基类。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 此接口不提供任何方法而非继承自`IDebugField`。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
