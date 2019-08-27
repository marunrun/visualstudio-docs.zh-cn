---
title: IDebugPointerObject3 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugPointerObject3 interface
ms.assetid: 11d26af4-1079-435e-96fa-d5269cbea8eb
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae6ec2f0ffc48e8c23f65ab56ec7b66d69d11a2e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440600"
---
# <a name="idebugpointerobject3"></a>IDebugPointerObject3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 表示在分析树中，指针并扩展**IDebugPointerObject**接口。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPointerObject3 : IDebugPointerObject  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器 (EE) 实现此接口。  
  
## <a name="methods"></a>方法  
 除了上的方法[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetPointerAddress](../../../extensibility/debugger/reference/idebugpointerobject3-getpointeraddress.md)|检索指针的地址。|  
  
## <a name="requirements"></a>要求  
 标头：Ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
