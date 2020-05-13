---
title: OPTNAMECHANGEPFN |微软文档
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
ms.openlocfilehash: 603bd08c1ec3832bf732e0b33101076738d009e3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702252"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
这是一个回调函数，在调用[SccSetOption（](../extensibility/sccsetoption-function.md)使用选项`SCC_OPT_NAMECHANGEPFN`）中指定，用于将源代码管理插件所做的名称更改传回 IDE。

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

[在]在以前调用[SccSetOption](../extensibility/sccsetoption-function.md)时指定的用户值（使用`SCC_OPT_USERDATA`选项 ）。

 pszOld名称

[在]文件的原始名称。

 psnewName

[在]文件重命名为的名称。

## <a name="return-value"></a>返回值
 无。

## <a name="remarks"></a>备注
 如果在源代码管理操作期间重命名了文件，源代码管理插件可以通过此回调通知 IDE有关名称更改。

 如果 IDE 不支持此回调，则不会调用[SccSetOption](../extensibility/sccsetoption-function.md)来指定它。 如果插件不支持此回调，则当 IDE 尝试设置回调时`SCC_E_OPNOTSUPPORTED`，它将`SccSetOption`从函数返回。

## <a name="see-also"></a>请参阅
- [IDE 实现的回调功能](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
