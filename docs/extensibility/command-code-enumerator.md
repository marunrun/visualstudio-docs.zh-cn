---
title: 命令代码枚举器 |Microsoft Docs
description: 命令代码枚举器用于 SccGetCommandOptions 和 SccPopulateListto 的选项，以指示为其指定了选项的命令。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 9a831813bb975819e9152dfab4d4eefd6b440606
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "94974254"
---
# <a name="command-code-enumerator"></a>命令代码枚举器
此枚举器用于 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 的选项和 [SccPopulateList](../extensibility/sccpopulatelist-function.md)，以指示为其指定了选项的命令。

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
SCC_COMMAND_GET 对应于 [SccGet](../extensibility/sccget-function.md)。

SCC_COMMAND_CHECKOUT 对应于 [SccCheckout](../extensibility/scccheckout-function.md)。

SCC_COMMAND_CHECKIN 对应于 [SccCheckin](../extensibility/scccheckin-function.md)。

SCC_COMMAND_UNCHECKOUT 对应于 [SccUncheckout](../extensibility/sccuncheckout-function.md)。

SCC_COMMAND_ADD 对应于 [SccAdd](../extensibility/sccadd-function.md)。

SCC_COMMAND_REMOVE 对应于 [SccRemove](../extensibility/sccremove-function.md)。

SCC_COMMAND_DIFF 对应于 [SccDiff](../extensibility/sccdiff-function.md)。

SCC_COMMAND_HISTORY 对应于 [SccHistory](../extensibility/scchistory-function.md)。

SCC_COMMAND_RENAME 对应于 [SccRename](../extensibility/sccrename-function.md)。

SCC_COMMAND_PROPERTIES 对应于 [SccProperties](../extensibility/sccproperties-function.md)。

SCC_COMMAND_OPTIONS 对应于 [SccSetOption](../extensibility/sccsetoption-function.md)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
