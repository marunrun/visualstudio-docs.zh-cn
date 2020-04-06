---
title: 目录状态代码枚举器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b5ebf61f2baa6e4277e27cd3c4d18a51e64f835
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712147"
---
# <a name="directory-status-code-enumerator"></a>目录状态代码枚举器
枚`SccDirStatus`举器包含指定的常量值，用于指定源控制系统中目录的状态。 此枚举由[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)使用。 这在源代码管理插件 API 的版本 1.2 中引入了。

## <a name="syntax"></a>语法

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>成员
 无法获得SCC_DIRSTATUS_INVALID状态;不要依赖它。

 SCC_DIRSTATUS_NOTCONTROLLED目录不受源代码管理。

 SCC_DIRSTATUS_CONTROLLED目录受源代码管理。

 SCC_DIRSTATUS_EMPTYPROJ与此目录对应的项目为空。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
