---
title: IDebugGenericFieldInstance |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldInstance interface
ms.assetid: f68b4761-be8b-4801-9d4b-cde90e01d95e
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8ab9c43e915f2c23dfe5f38ce61beff29949ca0e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180801"
---
# <a name="idebuggenericfieldinstance"></a>IDebugGenericFieldInstance
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示托管的代码的泛型类型的字段的一个实例。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugGenericFieldInstance : IUnknown  
```  
  
## <a name="methods"></a>方法  
 此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetTypeArguments](../../../extensibility/debugger/reference/idebuggenericfieldinstance-gettypearguments.md)|检索此实例的类型参数参数。|  
|[TypeArgumentCount](../../../extensibility/debugger/reference/idebuggenericfieldinstance-typeargumentcount.md)|返回此实例的参数自变量类型的数目。|  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
