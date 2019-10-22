---
title: IApplicationDebugger：： CreateInstanceAtDebugger |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.CreateInstanceAtDebugger
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::CreateInstanceAtDebugger
ms.assetid: 6763afac-c86a-4e88-9580-77108fb242fb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c15dc5d9b36a718ed41813bac46bc4b9415eb853
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577891"
---
# <a name="iapplicationdebuggercreateinstanceatdebugger"></a>IApplicationDebugger::CreateInstanceAtDebugger
允许通过在调试器中执行的代码在调试器进程中创建对象。  
  
> [!IMPORTANT]
> 不应实现此方法，因为它允许不受信任的代码在受信任的调试器线程中创建任意对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateInstanceAtDebugger(  
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
  
 当前未实现该方法。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)