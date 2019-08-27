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
ms.openlocfilehash: 64bcf6d443d1f96d650bde7fb92f69bbb12c5327
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353531"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 函数
此函数可更新特定的源控制命令的文件的列表，并提供所有给定文件的源代码管理状态。

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

[in]源控制插件上下文结构。

 nCommand

[in]将应用于所有文件的源控制命令`lpFileNames`数组 (请参阅[命令代码](../extensibility/command-code-enumerator.md)有关的可能的命令列表)。

 nFiles

[in]中的文件数`lpFileNames`数组。

 lpFileNames

[in]已知的 IDE 的文件名称的数组。

 pfnPopulate

[in]要调用以添加和删除文件的 IDE 回调函数 (请参阅[POPLISTFUNC](../extensibility/poplistfunc.md)有关详细信息)。

 pvCallerData

[in]要传递的值保持不变的回调函数。

 lpStatus

[in、 out]源代码管理插件返回的每个文件的状态标志的数组。

 fOptions

[in]命令标志 (请参阅的"PopulateList 标志"部分[位标志由特定命令](../extensibility/bitflags-used-by-specific-commands.md)有关详细信息)。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数将检查其当前状态的文件的列表。 它使用`pfnPopulate`回调函数，以通知调用方，当文件不匹配的条件时`nCommand`。 例如，如果该命令是`SCC_COMMAND_CHECKIN`并在列表中的文件未签出，然后使用回调来通知调用方。 有时，源代码管理插件可能会发现可以命令的一部分并将其添加其他文件。 这样，例如，Visual Basic 用户签出一个.bmp 文件，由其自己的项目，但没有显示在 Visual Basic 项目文件中。 用户选择**获取**命令在 IDE 中。 IDE 将显示它认为可以获取用户，所有文件的列表，但在该列表显示之前,`SccPopulateList`函数调用以确保要显示的列表是最新。

## <a name="example"></a>示例
 在 IDE 中生成它认为用户可以获取的文件的列表。 它将显示此列表之前，它会调用`SccPopulateList`函数中，为源代码管理插件提供到机会添加并从列表中删除文件。 插件通过调用给定的回调函数来修改列表 (请参阅[POPLISTFUNC](../extensibility/poplistfunc.md)的更多详细信息)。

 该插件将继续调用`pfnPopulate`函数，它将添加或删除文件，直到它完成，然后返回从`SccPopulateList`函数。 然后，IDE 可以显示其列表。 `lpStatus`数组均表示由 IDE 传入的原始列表中的所有文件。 回调函数的使用中的所有这些文件除了要让状态插件的填充。

> [!NOTE]
> 源代码管理插件始终可以选择只是此函数，因为它是离开列表立即返回。 如果插件实现此函数，则可以通过设置表示此`SCC_CAP_POPULATELIST`功能对的第一个调用中的位标志[SccInitialize](../extensibility/sccinitialize-function.md)。 默认情况下，该插件应始终假定要传入的所有项都是文件。 但是，如果 IDE 设置`SCC_PL_DIR`标记中`fOptions`参数中传递的所有项都都视为目录。 插件应在目录中添加属于的所有文件。 IDE 永远不会将传入文件和目录的混合。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [命令代码](../extensibility/command-code-enumerator.md)