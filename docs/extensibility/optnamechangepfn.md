---
title: OPTNAMECHANGEPFN |Microsoft Docs
description: 了解 OPTNAMECHANGEPFN 回调函数，该函数将名称更改从源代码管理插件传递到 Visual Studio IDE。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e18a3e5004a86bb96ad77112f4c81ebca3e59cbf
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863435"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
这是使用选项) 调用 [SccSetOption](../extensibility/sccsetoption-function.md) (指定的回调函数 `SCC_OPT_NAMECHANGEPFN` ，用于将源代码管理插件所做的名称更改传递回 IDE。

## <a name="signature"></a>签名

```cpp
typedef void (*OPTNAMECHANGEPFN)(
   LPVOID pvCallerData,
   LPCSTR pszOldName,
   LPCSTR pszNewName
);
```

## <a name="parameters"></a>参数
 pvCallerData

中使用 option) 在先前对 [SccSetOption](../extensibility/sccsetoption-function.md) (的调用中指定的用户值 `SCC_OPT_USERDATA` 。

 pszOldName

中文件的原始名称。

 pszNewName

中文件已重命名为的名称。

## <a name="return-value"></a>返回值
 无。

## <a name="remarks"></a>备注
 如果在源代码管理操作期间重命名了某个文件，则源代码管理插件可以通过此回调通知 IDE 有关名称更改的信息。

 如果 IDE 不支持此回调，则它将不会调用 [SccSetOption](../extensibility/sccsetoption-function.md) 来指定它。 如果插件不支持此回调，则在 `SCC_E_OPNOTSUPPORTED` `SccSetOption` IDE 尝试设置回调时，它将从函数返回。

## <a name="see-also"></a>另请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
