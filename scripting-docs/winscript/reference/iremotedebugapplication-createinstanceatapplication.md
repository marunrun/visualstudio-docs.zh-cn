---
title: IRemoteDebugApplication：： CreateInstanceAtApplication |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplication.CreateInstanceAtApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplication::CreateInstanceAtApplication
ms.assetid: d669ec80-2182-400d-87cc-7c1753315e5c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 285e5df6960e3188ffe1ce17b1fc4f43626a3d74
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572313"
---
# <a name="iremotedebugapplicationcreateinstanceatapplication"></a>IRemoteDebugApplication::CreateInstanceAtApplication
允许通过在应用程序中执行的代码在应用程序进程中创建对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateInstanceAtApplication(  
   REFCLSID    rclsid,  
   IUnknown*   pUnkOuter,  
   DWORD       dwClsContext,  
   REFIID      riid,  
   IUnknown**  ppvObject  
);  
```  
  
#### <a name="parameters"></a>参数  
 `rclsid`  
 中要创建的对象的类标识符（CLSID）。  
  
 `pUnkOuter`  
 中如果 `NULL`，则不会将对象作为聚合的一部分进行创建。 否则，`pUnkOuter` 是指向聚合对象的 `IUnknown` 接口（控制 `IUnknown`）的指针。  
  
 `dwClsContext`  
 中用于运行可执行代码的上下文。 这些值取自枚举 `CLSCTX`。  
  
 `riid`  
 中用于与对象通信的接口标识符。  
  
 `ppvObject`  
 弄指针变量的地址，该变量接收 `riid` 中请求的接口指针。 成功返回时，* `ppvObject` 包含请求的接口指针。 失败时，\* `ppvObject` 包含 `NULL`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法委托给 `CoCreateInstance`。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)