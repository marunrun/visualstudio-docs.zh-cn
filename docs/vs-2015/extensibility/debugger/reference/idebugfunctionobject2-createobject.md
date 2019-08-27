---
title: IDebugFunctionObject2::CreateObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b60801f5288e88795ab75145b9c6120d4308d1c7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202985"
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建使用给定评估标志设置和超时值的构造函数的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT CreateObject (  
   IDebugFunctionObject* pConstructor,  
   DWORD                 dwArgs,  
   IDebugObject*         pArgs[],  
   DWORD                 dwEvalFlags,  
   DWORD                 dwTimeout,  
   IDebugObject**        ppObject  
);  
```  
  
```csharp  
int CreateObject (  
   IDebugFunctionObject pConstructor,  
   uint                 dwArgs,  
   IDebugObject[]       pArgs,  
   uint                 dwEvalFlags,  
   uint                 dwTimeout,  
   out IDebugObject**   ppObject  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pConstructor`  
 [in][IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)对象，表示要创建的对象的构造函数。  
  
 `dwArgs`  
 [in]中的参数数量`pArg`数组。 表示传递给构造函数的参数数目。  
  
 `pArgs`  
 [in]一个数组[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)表示的参数的对象传递给构造函数。  
  
 `dwEvalFlags`  
 [in]中的标志的组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)指定计算的执行方式的枚举。  
  
 `dwTimeout`  
 [in]最大时间 （毫秒），此方法返回前等待。 使用**无限**无限期等待。  
  
 `ppObject`  
 [out]返回**IDebugObject**表示新创建的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法以创建一个对象，表示一个类或其他复杂类型，它需要是一个参数的构造函数的实例。  
  
## <a name="see-also"></a>请参阅  
 [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
