---
title: IDebugCoreServer3：：创建实例服务器 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2346bb76fe604265a309a51f48b734fc6f2ab8d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733021"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
在服务器上创建调试引擎的实例。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateInstanceInServer(
   LPCWSTR  szDll,
   WORD     wLangId,
   REFCLSID clsidObject,
   REFIID   riid,
   void**   ppvObject
);
```

```csharp
int CreateInstanceInServer(
   string     szDll,
   ushort     wLangID,
   ref Guid   clsidObject,
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>参数
`szDll`\
[在]实现参数中指定的 CLSID 的 dll`clsidObject`的路径。 如果是`NULL`，则调用 COM`CoCreateInstance`函数。

`wLangId`\
[在]调试引擎区域设置。 如果不应调用[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)方法，则此方法可以是 0。

`clsidObject`\
[在]要创建的调试引擎的 CLSID。

`riid`\
[在]要从类对象检索的特定接口的接口 ID。

`ppvObject`\
[出]`IUnknown`来自实例化对象的接口。 强制转换或封送此对象到所需的接口。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [设置区域设置](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)
