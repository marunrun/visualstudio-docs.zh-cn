---
title: 文件状态代码枚举器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94bd9ff93872139fc056c4c8bb7a59191616919e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342692"
---
# <a name="file-status-code-enumerator"></a>文件状态代码枚举器
`SccStatus`枚举数包含命名的常量值用于指定源代码管理系统中的文件的状态。 此枚举由[SccQueryInfo](../extensibility/sccqueryinfo-function.md)并`POPLISTFUNC`回调函数 (请参阅[POPLISTFUNC](../extensibility/poplistfunc.md)有关详细信息)。

## <a name="syntax"></a>语法

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>成员
 无法获取 SCC_STATUS_INVALID 状态;不依赖于它。

 SCC_STATUS_NOTCONTROLLED 文件不是源代码管理下。

 SCC_STATUS_CONTROLLED 文件处于源代码管理下。

 SCC_STATUS_CHECKEDOUT 签出在本地磁盘上的当前用户。

 由另一个用户签出 SCC_STATUS_OUTOTHER 文件。

 以独占方式签出 SCC_STATUS_OUTEXCLUSIVE 文件。

 通过多个用户签出 SCC_STATUS_OUTMULTIPLE 文件。

 SCC_STATUS_OUTOFDATE 文件不是最新的。

 已从项目删除 SCC_STATUS_DELETED 文件。

 SCC_STATUS_LOCKED 文件被锁定;不允许更多的版本。

 已合并 SCC_STATUS_MERGED 文件，但尚不支持固定/验证。

 项目之间共享 SCC_STATUS_SHARED 文件。

 SCC_STATUS_PINNED 文件共享到的显式版本。

 SCC_STATUS_MODIFIED 文件已修改/中断/违反。

 由当前用户签出 SCC_STATUS_OUTBYUSER 文件。

 SCC_STATUS_NOMERGE 文件永远不会与合并，无需在 GET 之前保存。

 SCC_STATUS_RESERVED_1 保留供内部使用。

 SCC_STATUS_RESERVED_2 保留供内部使用。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)