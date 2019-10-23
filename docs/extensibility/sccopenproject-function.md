---
title: SccOpenProject 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6aa4a715f8d1b87aa831f6a315f07a19e5d4f46
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721051"
---
# <a name="sccopenproject-function"></a>SccOpenProject 函数
此函数打开现有源代码管理项目或创建一个新项目。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccOpenProject (
   LPVOID        pvContext,
   HWND          hWnd,
   LPSTR         lpUser,
   LPCSTR        lpProjName,
   LPCSTR        lpLocalProjPath,
   LPSTR         lpAuxProjPath,
   LPCSTR        lpComment,
   LPTEXTOUTPROC lpTextOutProc,
   LONG          dwFlags
);
```

#### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpUser

[in，out]用户的名称（不能超过 SCC_USER_SIZE，包括 NULL 终止符）。

 lpProjName

中标识项目名称的字符串。

 lpLocalProjPath

中项目的工作文件夹的路径。

 lpAuxProjPath

[in，out]标识项目的可选辅助字符串（不能超过 SCC_AUXPATH_SIZE，包括 NULL 终止符）。

 lpComment

中为正在创建的新项目添加注释。

 lpTextOutProc

中用于显示源代码管理插件文本输出的可选回调函数。

 dwFlags

中指示当项目对于源代码管理插件未知时是否需要创建一个新项目。 值可以是 `SCC_OP_CREATEIFNEW` 和 `SCC_OP_SILENTOPEN.` 的组合

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|打开项目成功。|
|SCC_E_INITIALIZEFAILED|项目无法初始化。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|在调用之前，该项目不存在; 已设置 `SCC_OPT_CREATEIFNEW` 标志，但无法创建项目。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_UNKNOWNPROJECT|项目对于源代码管理插件是未知的，未设置 `SCC_OPT_CREATEIFNEW` 标志。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECFICERROR|不特定的失败;源代码管理系统未初始化。|

## <a name="remarks"></a>备注
 IDE 可能会传入用户名（`lpUser`），也可能只是传入指向空字符串的指针。 如果存在用户名，则源代码管理插件应该使用该用户名作为默认值。 但是，如果未传递任何名称，或者登录失败，则该插件应该提示用户登录，并将在收到有效的登录 `.` 时返回 `lpUser` 中的有效名称，因为该插件可能会更改用户名字符串，IDE 将始终分配大小为的缓冲区（`SCC_USER_LEN` + 1 或 SCC_USER_SIZE，其中包含 null 终止符的空间）。

> [!NOTE]
> IDE 可能需要执行的第一个操作可能是调用 `SccOpenProject` 函数或[SccGetProjPath](../extensibility/sccgetprojpath-function.md)。 出于此原因，它们都具有相同的 `lpUser` 参数。

 `lpAuxProjPath` 和 `lpProjName` 从解决方案文件中读取，或从对 `SccGetProjPath` 函数的调用返回。 这些参数包含源代码管理插件与项目关联的字符串，仅对插件有意义。 如果解决方案文件中没有此类字符串，并且未提示用户浏览（这会通过 `SccGetProjPath` 函数返回一个字符串），IDE 将同时传递 `lpAuxProjPath` 和 `lpProjName` 的空字符串，并期望插件在第is 函数返回。

 `lpTextOutProc` 是指向 IDE 为源代码管理插件提供的回调函数的指针，用于显示命令结果输出。 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)中详细介绍了此回调函数。

> [!NOTE]
> 如果源代码管理插件打算利用此方法，则必须在[SccInitialize](../extensibility/sccinitialize-function.md)中设置 `SCC_CAP_TEXTOUT` 标志。 如果未设置该标志，或者如果 IDE 不支持此功能，则将 `NULL` `lpTextOutProc`。

 @No__t_0 参数控制正在打开的项目当前不存在的结果。 它包含两个 bitflags、`SCC_OP_CREATEIFNEW` 和 `SCC_OP_SILENTOPEN`。 如果要打开的项目已存在，则该函数只会打开项目并返回 `SCC_OK`。 如果项目不存在并且 `SCC_OP_CREATEIFNEW` 标志为 on，则源代码管理插件可以在源代码管理系统中创建项目，打开该项目，然后返回 `SCC_OK`。 如果该项目不存在，并且 `SCC_OP_CREATEIFNEW` 标志为 off，则该插件随后应检查 `SCC_OP_SILENTOPEN` 标志。 如果该标志未打开，则插件可能会提示用户输入项目名称。 如果启用该标志，则该插件应该只返回 `SCC_E_UNKNOWNPROJECT`。

## <a name="calling-order"></a>调用顺序
 在正常事件的过程中，将首先调用[SccInitialize](../extensibility/sccinitialize-function.md)以打开源代码管理会话。 会话可能包含对 `SccOpenProject` 的调用，后跟其他源代码管理插件 API 函数调用，并将通过调用[SccCloseProject](../extensibility/scccloseproject-function.md)而终止。 此类会话可能会在调用[SccUninitialize](../extensibility/sccuninitialize-function.md)之前重复多次。

 如果源代码管理插件在 `SccInitialize` 中设置 `SCC_CAP_REENTRANT` 位，则上述会话序列可能会并行重复多次。 不同 `pvContext` 结构跟踪不同会话，其中每个 `pvContext` 一次与一个打开的项目相关联。 根据 `pvContext` 参数，该插件可以确定在任何特定调用中引用的项目。 如果未设置功能位 `SCC_CAP_REENTRANT`，则 nonreentrant 源代码管理插件在处理多个项目的能力方面受到限制。

> [!NOTE]
> 源代码管理插件 API 1.1 版中引入了 `SCC_CAP_REENTRANT` 位。 在版本1.0 中未设置或已忽略，并且假定所有版本1.0 源代码管理插件都是 nonreentrant。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)