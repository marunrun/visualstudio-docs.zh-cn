---
title: SccGetCommandOptions 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eeefa26422476ca40e782df3ff35eee9d429a149
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700835"
---
# <a name="sccgetcommandoptions-function"></a>SccGetCommandOptions 函数
此函数提示用户输入给定命令的高级选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetCommandOptions(
   LPVOID pvContext,
   HWND hWnd,
   enum SCCCOMMAND iCommand,
   LPCMDOPTS* ppvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 iCommand

中请求高级选项的命令 (参阅) 可能值的 [命令代码](../extensibility/command-code-enumerator.md) 。

 ppvOptions

中还可以) 选项结构 (`NULL` 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_I_ADV_SUPPORT|源代码管理插件支持命令的高级选项。|
|SCC_I_OPERATIONCANCELED|用户取消了源代码管理插件的 " **选项** " 对话框。|
|SCC_E_OPTNOTSUPPORTED|源代码管理插件不支持此操作。|
|SCC_E_ISCHECKEDOUT|无法对当前签出的文件执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 IDE 首次调用此函数 `ppvOptions` = `NULL` 以确定源代码管理插件是否支持指定命令的高级选项功能。 如果插件支持该命令的功能，则 IDE 会在用户请求高级选项时再次调用此函数， (通常作为对话框中的 " **高级** " 按钮实现) 并提供指向指针的非 NULL 指针 `ppvOptions` `NULL` 。 插件将用户指定的任何高级选项存储在私有结构中，并返回指向中该结构的指针 `ppvOptions` 。 然后，将此结构传递给需要了解的所有其他源代码管理插件 API 函数，包括对函数的后续调用 `SccGetCommandOptions` 。

 例如，可以帮助阐明这种情况。

 用户选择 **get** 命令，IDE 将显示 " **获取** " 对话框。 IDE 调用 `SccGetCommandOptions` 函数， `iCommand` 并将设置为 `SCC_COMMAND_GET` 并 `ppvOptions` 将设置为 `NULL` 。 源代码管理插件将此解释为 "你是否有此命令的任何高级选项？" 如果插件返回 `SCC_I_ADV_SUPPORT` ，IDE 将在 "**获取**" 对话框中显示 "**高级**" 按钮。

 用户第一次单击 " **高级** " 按钮时，IDE 将再次调用该 `SccGetCommandOptions` 函数，这一次是指指向 `NULL``ppvOptions` 指针的非 `NULL` 。 该插件将显示其自己的 " **获取选项** " 对话框，提示用户输入信息，将该信息放入其自身的结构，并返回指向中该结构的指针 `ppvOptions` 。

 如果用户在同一对话框中再次单击 " **高级** "，则 IDE 将 `SccGetCommandOptions` 再次调用函数而不进行更改 `ppvOptions` ，以便将结构传递回插件。 这使插件能够将其对话框重新初始化为用户以前设置的值。 在返回之前，该插件会就地修改结构。

 最后，当用户在 IDE 的 "**获取**" 对话框中单击 **"确定"** 时，ide 将调用[SccGet](../extensibility/sccget-function.md)，同时传递中返回的 `ppvOptions` 包含高级选项的结构。

> [!NOTE]
> `SCC_COMMAND_OPTIONS`当 IDE 显示 "**选项**" 对话框时，使用该命令来设置控制集成工作方式的首选项。 如果源代码管理插件希望提供其自己的首选项对话框，它可以在 IDE 的 "首选项" 对话框中的 " **高级** " 按钮上显示。 该插件仅负责获取和保存此信息;IDE 不会使用或修改它。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [命令代码](../extensibility/command-code-enumerator.md)
