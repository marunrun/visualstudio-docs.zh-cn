---
title: IDebugDynamicFieldCOMPlus | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 71756b4c4df0768520f72219cf50e5407604635d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198503"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示有关动态字段[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugDynamicFieldCOMPlus : IDebugDynamicField  
```  
  
## <a name="methods"></a>方法  
 除了上的方法[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|检索给定其基元类型的类型。|  
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|检索在给定其标记的类型。|  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
