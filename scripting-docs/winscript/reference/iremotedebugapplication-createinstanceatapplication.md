---
title: IRemoteDebugApplication::CreateInstanceAtApplication | Microsoft Docs
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
ms.openlocfilehash: 6e17c5abcb21bfaad6de948c3676d29232da66cf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944314"
---
# <a name="iremotedebugapplicationcreateinstanceatapplication"></a>IRemoteDebugApplication::CreateInstanceAtApplication
通过代码允许应用程序进程中的对象的创建，它是-进程外对应用程序。  
  
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
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)