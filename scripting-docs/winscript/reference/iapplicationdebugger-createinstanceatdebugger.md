---
title: IApplicationDebugger::CreateInstanceAtDebugger |Microsoft Docs
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
ms.openlocfilehash: 95489464128e706e755432bee991c5481f5af8bc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63425830"
---
# <a name="iapplicationdebuggercreateinstanceatdebugger"></a>IApplicationDebugger::CreateInstanceAtDebugger
通过代码在调试器进程中允许创建的对象，它是-进程外调试器。  
  
> [!IMPORTANT]
> 不应实现此方法，因为它允许不受信任的代码中的受信任的调试程序线程创建任意对象。  
  
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
 [in]要创建的对象标识符 (CLSID) 的类。  
  
 `pUnkOuter`  
 [in]如果`NULL`，并未创建该对象为一个聚合的组成部分。 否则为`pUnkOuter`是指向聚合对象的指针`IUnknown`接口 (控制`IUnknown`)。  
  
 `dwClsContext`  
 [in]运行可执行代码的上下文。 值取自枚举`CLSCTX`。  
  
 `riid`  
 [in]使用与对象进行通信的接口标识符。  
  
 `ppvObject`  
 [out]接收请求中的接口指针的指针变量的地址`riid`。 在成功返回时，*`ppvObject`包含请求的接口指针。 如果失败， \* `ppvObject`包含`NULL`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法委托给`CoCreateInstance`。  
  
 目前尚未实现该方法。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)