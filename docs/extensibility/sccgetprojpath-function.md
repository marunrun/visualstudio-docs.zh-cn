---
title: SccGetProjPath 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 281787da3499c081fbbe6f59b7b8175a4dbf24d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700695"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 函数
此函数提示用户提供项目路径，该路径是仅对源代码管理插件有意义的字符串。 当用户：

- 创建新项目

- 将现有项目添加到版本控制

- 正在尝试查找现有版本控制项目

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetProjPath (
   LPVOID pvContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPSTR  lpProjName,
   LPSTR  lpLocalPath,
   LPSTR  lpAuxProjPath,
   BOOL   bAllowChangePath,
   LPBOOL pbNew
);
```

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpUser

[in，out]用户名不能超过 SCC_USER_SIZE （包括 NULL 终止符） () 

 lpProjName

[in，out]IDE 项目、项目工作区或生成文件的名称不 (超过 SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpLocalPath

[in，out]项目的工作路径。 如果 `bAllowChangePath` 为 `TRUE` ，则源代码管理插件可以修改此字符串 (不能超过 _MAX_PATH，包括 null 终止符) 。

 lpAuxProjPath

[in，out]返回的项目路径的缓冲区 (不能超过 SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 bAllowChangePath

中如果这是 `TRUE` ，则源代码管理插件可以提示并修改 `lpLocalPath` 字符串。

 pbNew

[in，out]传入的值指示是否创建新的项目。 返回的值表示创建项目成功：

|传入|解释|
|--------------|--------------------|
|TRUE|用户可以创建新项目。|
|FALSE|用户可能不会创建新项目。|

|传出|解释|
|--------------|--------------------|
|TRUE|已创建新项目。|
|FALSE|已选择现有项目。|

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功创建或检索项目。|
|SCC_I_OPERATIONCANCELED|该操作已取消。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_CONNECTIONFAILURE|尝试连接到源代码管理系统时出现问题。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此函数的目的是让 IDE 获取参数 `lpProjName` 和 `lpAuxProjPath` 。 源代码管理插件提示用户输入此信息后，它会将这两个字符串传递回 IDE。 IDE 将这些字符串保存在其解决方案文件中，并在用户打开此项目时将它们传递给 [SccOpenProject](../extensibility/sccopenproject-function.md) 。 这些字符串使插件可以跟踪与项目关联的信息。

 第一次调用函数时，将 `lpAuxProjPath` 设置为空字符串。 `lProjName` 也可以为空，也可以包含 IDE 项目名称，源代码管理插件可以使用或忽略该名称。 当函数成功返回时，插件将返回两个对应的字符串。 IDE 不会对这些字符串进行任何假设，不会使用它们，也不会允许用户修改它们。 如果用户想要更改设置，则 IDE 将 `SccGetProjPath` 再次调用，并传入以前收到的相同值。 这使插件能够完全控制这两个字符串。

 对于 `lpUser` ，IDE 可能会传入用户名，也可能只是传入指向空字符串的指针。 如果存在用户名，则源代码管理插件应该使用该用户名作为默认值。 但是，如果未传递任何名称，或者登录失败，且具有给定名称，则插件应该提示用户输入登录名，并在收到有效的登录名后将该名称传回 `lpUser` 。 因为插件可能会更改此字符串，所以 IDE 将始终 (+ 1) 分配大小的缓冲区 `SCC_USER_LEN` 。

> [!NOTE]
> IDE 执行的第一个操作可能是对 `SccOpenProject` 函数或函数的调用 `SccGetProjPath` 。 因此，这两个参数都有一个相同的 `lpUser` 参数，该参数使源代码管理插件可以在任何时间记录用户。 即使从函数返回表示失败，该插件也必须使用有效的登录名填充此字符串。

 `lpLocalPath` 用户在其中保留项目的目录。 它可以是空字符串。 如果当前未定义任何目录 (例如，如果用户尝试从源代码管理) 系统下载项目，则为 `bAllowChangePath` ; 如果为 `TRUE` ，则源代码管理插件可以提示用户输入，或使用其他方法将其自身的字符串放入中 `lpLocalPath` 。 如果 `bAllowChangePath` 为 `FALSE` ，则插件不应更改字符串，因为用户已在指定的目录中工作。

 如果用户创建要置于源代码管理下的新项目，则源代码管理插件可能不会在调用时在源代码管理系统中实际创建该项目 `SccGetProjPath` 。 相反，它将返回字符串以及的非零值 `pbNew` ，指示将在源代码管理系统中创建项目。

 例如，如果 Visual Studio 中的 " **新建项目** " 向导中的用户将其项目添加到源代码管理中，则 visual studio 将调用此函数，并且该插件将确定是否可以在源代码管理系统中创建新项目以包含 Visual Studio 项目。 如果用户在完成向导之前单击 " **取消** "，则永远不会创建该项目。 如果用户单击 **"确定"**，则 Visual Studio `SccOpenProject` 将调用 `SCC_OPT_CREATEIFNEW` 并传入，并且此时会创建源代码管理的项目。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
