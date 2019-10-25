---
title: SccPopulateList 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a2cfdf5a617352d7ba0c2db00e7705343f1eb5e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720872"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 函数
此函数更新特定源代码管理命令的文件列表，并提供所有给定文件的源代码管理状态。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccPopulateList (
   LPVOID          pvContext,
   enum SCCCOMMAND nCommand,
   LONG            nFiles,
   LPCSTR*         lpFileNames,
   POPLISTFUNC     pfnPopulate,
   LPVOID          pvCallerData,
   LPLONG          lpStatus,
   LONG            fOptions
);
```

#### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 N 命令

中将应用于 `lpFileNames` 数组中所有文件的源代码管理命令（有关可能命令的列表，请参阅[命令代码](../extensibility/command-code-enumerator.md)）。

 n

中@No__t_0 数组中的文件数。

 lpFileNames

中IDE 已知的文件名的数组。

 pfnPopulate

中用于调用以添加和删除文件的 IDE 回调函数（有关详细信息，请参阅[POPLISTFUNC](../extensibility/poplistfunc.md) ）。

 pvCallerData

中将以不更改的形式传递给回调函数的值。

 lpStatus

[in，out]用于源控件插件的数组，用于返回每个文件的状态标志。

 用于

中命令标志（有关详细信息，请参阅[特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md)的 "PopulateList 标志" 部分）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数检查文件的列表中是否有当前状态。 当文件与 `nCommand` 的条件不匹配时，它将使用 `pfnPopulate` 回调函数通知调用方。 例如，如果命令为 `SCC_COMMAND_CHECKIN` 并且列表中的某个文件未签出，则使用回调来通知调用方。 有时，源代码管理插件可能会找到可能是命令的一部分并添加的其他文件。 例如，这允许 Visual Basic 用户签出其项目使用但未出现在 Visual Basic 项目文件中的 .bmp 文件。 用户选择 IDE 中的**Get**命令。 IDE 将显示它认为用户可以获取的所有文件的列表，但在显示列表之前，将调用 `SccPopulateList` 函数以确保显示的列表是最新的。

## <a name="example"></a>示例
 IDE 将生成它认为用户可以获取的文件的列表。 在显示此列表之前，它将调用 `SccPopulateList` 函数，使源代码管理插件可以在列表中添加和删除文件。 该插件通过调用给定的回调函数来修改列表（有关详细信息，请参阅[POPLISTFUNC](../extensibility/poplistfunc.md) ）。

 插件继续调用 `pfnPopulate` 函数，该函数将添加和删除文件，直到它完成，然后从 `SccPopulateList` 函数返回。 然后，IDE 可以显示其列表。 @No__t_0 数组表示由 IDE 传入的原始列表中的所有文件。 插件除了使用回调函数外，还会填充所有这些文件的状态。

> [!NOTE]
> 源代码管理插件始终可以选择直接从该函数返回，使列表保持原样。 如果插件实现了此函数，则可以通过在对[SccInitialize](../extensibility/sccinitialize-function.md)的第一次调用中设置 `SCC_CAP_POPULATELIST` 功能位标志来指示这一点。 默认情况下，插件应始终假定传入的所有项都是文件。 但是，如果 IDE 在 `fOptions` 参数中设置了 `SCC_PL_DIR` 标志，则传入的所有项都将被视为目录。 此插件应该添加目录中的所有文件。 IDE 将永远不会传入文件和目录。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [命令代码](../extensibility/command-code-enumerator.md)