---
title: IDebugExtendedField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugExtendedField interface
ms.assetid: b491499c-af57-47da-87d6-34b7398f6591
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8001ced3ba2116ec8ff76ecdac2d0789304335e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62547242"
---
# <a name="idebugextendedfield"></a>IDebugExtendedField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

扩展了可用于支持托管的代码泛型的字段的类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugExtendedField : IDebugField  
```  
  
## <a name="methods"></a>方法  
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)|检索指定扩展的字段类型。|  
|[IsClosedType](../../../extensibility/debugger/reference/idebugextendedfield-isclosedtype.md)|确定是否该字段表示封闭的类型。|  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
