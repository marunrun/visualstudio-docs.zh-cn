---
title: 文件状态代码枚举器 |微软文档
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
ms.openlocfilehash: 184c8686ea184aea2cbd0a64873718cbe72f7615
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711456"
---
# <a name="file-status-code-enumerator"></a>文件状态代码枚举器
枚`SccStatus`举器包含指定的常量值，用于指定源控制系统中文件的状态。 此枚举由[SccQueryInfo](../extensibility/sccqueryinfo-function.md)和`POPLISTFUNC`回调函数使用（有关详细信息，请参阅[POPLISTFUNC）。](../extensibility/poplistfunc.md)

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
 无法获得SCC_STATUS_INVALID状态;不要依赖它。

 SCC_STATUS_NOTCONTROLLED文件不受源代码管理。

 SCC_STATUS_CONTROLLED文件处于源代码管理之下。

 SCC_STATUS_CHECKEDOUT本地磁盘上的当前用户签出。

 SCC_STATUS_OUTOTHER文件由其他用户签出。

 SCC_STATUS_OUTEXCLUSIVE文件被完全签出。

 SCC_STATUS_OUTMULTIPLE文件由多个用户签出。

 SCC_STATUS_OUTOFDATE 该文件不是最新的。

 SCC_STATUS_DELETED文件已从项目中删除。

 SCC_STATUS_LOCKED文件已锁定;不允许更多版本。

 SCC_STATUS_MERGED文件已合并但尚未修复/验证。

 SCC_STATUS_SHARED文件在项目之间共享。

 SCC_STATUS_PINNED文件共享到显式版本。

 SCC_STATUS_MODIFIED文件已被修改/损坏/违反。

 SCC_STATUS_OUTBYUSER文件由当前用户签出。

 SCC_STATUS_NOMERGE文件永远不能与 GET 合并，也不需要在 GET 之前保存。

 SCC_STATUS_RESERVED_1保留供内部使用。

 SCC_STATUS_RESERVED_2保留供内部使用。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
