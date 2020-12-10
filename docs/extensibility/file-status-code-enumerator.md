---
title: 文件状态代码枚举器 |Microsoft Docs
description: SccStatus 枚举器包含的常量值用于指定源代码管理系统中的文件状态，由 SccQueryInfo 和 POPLISTFUNC 使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0093e3a79a5a9caf9846c4b418226568e37828f0
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994480"
---
# <a name="file-status-code-enumerator"></a>文件状态代码枚举器
`SccStatus`枚举器包含指定源代码管理系统中文件状态的命名常量值。 此枚举由 [SccQueryInfo](../extensibility/sccqueryinfo-function.md) 和 `POPLISTFUNC` 回调函数使用 (请参阅 [POPLISTFUNC](../extensibility/poplistfunc.md) 了解详细信息) 。

## <a name="syntax"></a>语法

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>成员
 无法获取 SCC_STATUS_INVALID 状态;不要依赖于它。

 SCC_STATUS_NOTCONTROLLED 文件不受源代码管理。

 SCC_STATUS_CONTROLLED 文件受源代码管理。

 当前用户已在本地磁盘上签出 SCC_STATUS_CHECKEDOUT。

 SCC_STATUS_OUTOTHER 文件已由其他用户签出。

 SCC_STATUS_OUTEXCLUSIVE 文件以独占方式签出。

 SCC_STATUS_OUTMULTIPLE 多个用户签出了该文件。

 SCC_STATUS_OUTOFDATE 文件不是最新的。

 SCC_STATUS_DELETED 文件已从项目中删除。

 锁定 SCC_STATUS_LOCKED 文件;不允许更多版本。

 SCC_STATUS_MERGED 文件已合并，但尚未修复/验证。

 SCC_STATUS_SHARED 文件在项目之间共享。

 SCC_STATUS_PINNED 文件共享到显式版本。

 SCC_STATUS_MODIFIED 文件已修改/损坏/违反。

 SCC_STATUS_OUTBYUSER 文件由当前用户签出。

 SCC_STATUS_NOMERGE 文件永远不能与合并，并且无需在 GET 之前保存。

 SCC_STATUS_RESERVED_1 保留供内部使用。

 SCC_STATUS_RESERVED_2 保留供内部使用。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
