---
title: SccGet命令选项功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700835"
---
# <a name="sccgetcommandoptions-function"></a>SccGet命令选项功能
此函数提示用户为给定命令提供高级选项。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 iCommand

[在]请求高级选项的命令（有关可能的值，请参阅[命令代码](../extensibility/command-code-enumerator.md)）。

 ppvOptions

[在]选项结构（也可以为`NULL`）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_I_ADV_SUPPORT|源代码管理插件支持命令的高级选项。|
|SCC_I_OPERATIONCANCELED|用户取消了源代码管理插件的 **"选项"** 对话框。|
|SCC_E_OPTNOTSUPPORTED|源代码管理插件不支持此操作。|
|SCC_E_ISCHECKEDOUT|无法对当前签出的文件执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 IDE 首次`ppvOptions`=`NULL`调用此函数，以确定源代码管理插件是否支持指定命令的高级选项功能。 如果插件确实支持该命令的功能，则当用户请求高级选项（通常在对话框中作为**高级**按钮实现）并为`ppvOptions`该指针`NULL`提供非 NULL 指针时，IDE 将再次调用此函数。 该插件将用户指定的任何高级选项存储在私有结构中，并在 中返回指向该结构的`ppvOptions`指针。 然后，此结构将传递给所有其他源代码管理插件 API 函数，这些函数需要了解它，包括随后对函数的`SccGetCommandOptions`调用。

 一个例子可能有助于澄清这种情况。

 用户选择 **"获取"** 命令，IDE 将显示 **"获取"** 对话框。 IDE 调用设置为`SccGetCommandOptions``iCommand``SCC_COMMAND_GET`和`ppvOptions`设置为`NULL`的函数。 源代码管理插件将此解释为"您对此命令是否有任何高级选项？ 如果插件返回`SCC_I_ADV_SUPPORT`，IDE 在其 **"获取"** 对话框中显示**一个高级**按钮。

 用户首次单击 **"高级"** 按钮时，IDE 将再次调用`SccGetCommandOptions`该函数，这一次使用指向`NULL``ppvOptions``NULL`指针的非函数。 该插件显示其自己的 **"获取选项"** 对话框，提示用户提供信息，将该信息放入其自己的结构，并在 中返回指向该结构的`ppvOptions`指针。

 如果用户在同一对话框中再次单击 **"高级"，IDE**将再次调用`SccGetCommandOptions`该函数而不更改`ppvOptions`，以便结构传回插件。 这使插件能够将其对话框重新初始化到用户以前设置的值。 插件在返回之前修改就地的结构。

 最后，当用户单击 IDE 的 **"获取"** 对话框中的 **"确定"** 时，IDE 将调用[SccGet，](../extensibility/sccget-function.md)传递返回的结构`ppvOptions`，其中包含高级选项。

> [!NOTE]
> 当`SCC_COMMAND_OPTIONS`IDE 显示**选项**对话框，允许用户设置控制集成工作方式的首选项时，将使用该命令。 如果源代码管理插件想要提供自己的首选项对话框，则可以从 IDE 首选项对话框中的 **"高级"** 按钮显示它。 插件完全负责获取和保留此信息;IDE 不使用或修改它。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [命令代码](../extensibility/command-code-enumerator.md)
