---
title: 放大缩小字体功能 放大缩小字体功能微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f518413adba1546bcff4f7cf2e62b4563cf1bcc7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700534"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 函数
此函数更新特定源代码管理命令的文件列表，并在所有给定文件上提供源代码管理状态。

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

[在]源代码管理插件上下文结构。

 nCommand

[在]将应用于`lpFileNames`数组中的所有文件的源代码控制命令（有关可能的命令列表，请参阅[命令代码](../extensibility/command-code-enumerator.md)）。

 n文件

[在]数组中`lpFileNames`的文件数。

 lpFile名称

[在]IDE 已知的文件名数组。

 pfn 填充

[在]用于调用以添加和删除文件的 IDE 回调函数（有关详细信息，请参阅[POPLISTFUNC）。](../extensibility/poplistfunc.md)

 pvCallerData

[在]要传递给回调函数的值保持不变。

 lp状态

[进出]源控件插件的数组，用于返回每个文件的状态标志。

 fOptions

[在]命令标志（有关详细信息，请参阅[特定命令使用的位标志的](../extensibility/bitflags-used-by-specific-commands.md)"填充列表标志"部分）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 此函数检查文件列表的当前状态。 当文件与`pfnPopulate`的条件`nCommand`不匹配时，它使用回调函数通知调用方。 例如，如果命令是`SCC_COMMAND_CHECKIN`，并且列表中的文件未签出，则回调用于通知调用方。 有时，源代码管理插件可能会找到其他文件，这些文件可能是命令的一部分，并添加它们。 例如，这允许 Visual Basic 用户签出其项目使用的 .bmp 文件，但不显示在 Visual Basic 项目文件中。 用户在 IDE 中选择 **"获取**"命令。 IDE 将显示它认为用户可以获取的所有文件的列表，但在显示列表之前，将调用该`SccPopulateList`函数以确保要显示的列表是最新的。

## <a name="example"></a>示例
 IDE 生成它认为用户可以获取的文件列表。 在显示此列表之前，它会调用`SccPopulateList`该函数，使源代码管理插件有机会从列表中添加和删除文件。 插件通过调用给定的回调函数来修改列表（有关详细信息，请参阅[POPLISTFUNC）。](../extensibility/poplistfunc.md)

 插件继续调用`pfnPopulate`函数，该函数添加和删除文件，直到它完成，然后从函数`SccPopulateList`返回。 然后，IDE 可以显示其列表。 数组`lpStatus`表示 IDE 传入的原始列表中的所有文件。 除了使用回调功能外，插件还填充所有这些文件的状态。

> [!NOTE]
> 源代码管理插件始终可以选择立即从此函数返回，使列表保留为现在。 如果插件实现此函数，它可以通过在[Scc初始化](../extensibility/sccinitialize-function.md)的第一`SCC_CAP_POPULATELIST`个调用中设置功能位标志来指示这一点。 默认情况下，插件应始终假定传入的所有项目都是文件。 但是，如果 IDE 在`SCC_PL_DIR``fOptions`参数中设置标志，则传入的所有项都将被视为目录。 插件应添加属于目录中的所有文件。 IDE 永远不会传递文件和目录的混合。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [命令代码](../extensibility/command-code-enumerator.md)
