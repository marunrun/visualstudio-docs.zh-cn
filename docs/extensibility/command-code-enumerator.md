---
title: 命令代码枚举器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15916d26ac0120417205af0bb9117a45ec0397c6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739796"
---
# <a name="command-code-enumerator"></a>命令代码枚举器
此枚举器用于[SccGetCommandOptions 和](../extensibility/sccgetcommandoptions-function.md) [Scc 填充列表](../extensibility/sccpopulatelist-function.md)的选项中，以指示为其指定选项的命令。

## <a name="syntax"></a>语法

```
enum SCCCOMMAND {
   SCC_COMMAND_GET,
   SCC_COMMAND_CHECKOUT,
   SCC_COMMAND_CHECKIN,
   SCC_COMMAND_UNCHECKOUT,
   SCC_COMMAND_ADD,
   SCC_COMMAND_REMOVE,
   SCC_COMMAND_DIFF,
   SCC_COMMAND_HISTORY,
   SCC_COMMAND_RENAME,
   SCC_COMMAND_PROPERTIES,
   SCC_COMMAND_OPTIONS
};
```

## <a name="members"></a>成员
SCC_COMMAND_GET对应于[SccGet。](../extensibility/sccget-function.md)

SCC_COMMAND_CHECKOUT对应于[SccCheckout。](../extensibility/scccheckout-function.md)

SCC_COMMAND_CHECKIN对应于[SccCheckin。](../extensibility/scccheckin-function.md)

SCC_COMMAND_UNCHECKOUT对应于[SccUncheck。](../extensibility/sccuncheckout-function.md)

SCC_COMMAND_ADD对应于[SccAdd](../extensibility/sccadd-function.md)。

SCC_COMMAND_REMOVE对应于[SccRemove](../extensibility/sccremove-function.md)。

SCC_COMMAND_DIFF对应于[SccDiff](../extensibility/sccdiff-function.md)。

SCC_COMMAND_HISTORY对应于[史抄](../extensibility/scchistory-function.md)

SCC_COMMAND_RENAME对应于[SccRename](../extensibility/sccrename-function.md)。

SCC_COMMAND_PROPERTIES对应于[Scc属性](../extensibility/sccproperties-function.md)。

SCC_COMMAND_OPTIONS对应于[SccSetOption](../extensibility/sccsetoption-function.md)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
