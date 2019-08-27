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
ms.openlocfilehash: ebb8f4250b4ef4c022c5c21d748e025ca31e35a7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353603"
---
# <a name="sccopenproject-function"></a>SccOpenProject 函数
此函数将打开现有的源代码管理项目，或创建一个新。

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 lpUser

[in、 out]用户 （不超过 SCC_USER_SIZE，包括 NULL 终止符） 的名称。

 lpProjName

[in]标识项目的名称的字符串。

 lpLocalProjPath

[in]到项目的工作文件夹路径。

 lpAuxProjPath

[in、 out]一个可选的辅助字符串，用于标识项目 （不超过 SCC_AUXPATH_SIZE，包括 NULL 终止符）。

 lpComment

[in]正在创建一个新项目的注释。

 lpTextOutProc

[in]要显示文本输出从源代码管理插件的可选的回调函数。

 dwFlags

[in]信号需要如果项目是未知的源创建一个新的项目是否控制插件。 值可以是组合的`SCC_OP_CREATEIFNEW`和 `SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|在中打开项目的成功。|
|SCC_E_INITIALIZEFAILED|无法初始化项目。|
|SCC_E_INVALIDUSER|用户不可以登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|项目不存在之前调用; `SCC_OPT_CREATEIFNEW`设置标志，但无法创建项目。|
|SCC_E_PROJSYNTAXERR|无效的项目的语法。|
|SCC_E_UNKNOWNPROJECT|项目是未知的源代码管理插件，和`SCC_OPT_CREATEIFNEW`未设置标志。|
|SCC_E_INVALIDFILEPATH|无效或不可用的文件路径。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NONSPECFICERROR|非特定的失败;未初始化源代码管理系统。|

## <a name="remarks"></a>备注
 IDE 可能通过在用户名中 (`lpUser`)，或者它可能只是一个指针传递到一个空字符串。 如果用户名称，源代码管理插件应使用它作为默认值。 但是，如果未传递名称，或者如果具有给定名称的登录失败，该插件应提示用户登录并将返回中的有效名称`lpUser`当它收到有效的登录名`.`由于插件可能会更改用户名称字符串IDE 会始终分配大小的缓冲区 (`SCC_USER_LEN`+ 1 或 SCC_USER_SIZE，其中包括 null 终止符的占用空间)。

> [!NOTE]
> IDE 所要执行的第一个操作可能是对的调用`SccOpenProject`函数或[SccGetProjPath](../extensibility/sccgetprojpath-function.md)。 出于此原因，它们都具有相同`lpUser`参数。

 `lpAuxProjPath` 并`lpProjName`读取从解决方案文件，或它们返回到调用`SccGetProjPath`函数。 这些参数包含源代码管理插件将与项目相关联的字符串，并且仅对插件有意义。 如果没有此类字符串是在解决方案文件，并且用户不会提示以浏览 (这会返回一个字符串，通过`SccGetProjPath`函数)，IDE 将空字符串传递两个`lpAuxProjPath`和`lpProjName`，并需要更新这些值通过插件时，此函数返回。

 `lpTextOutProc` 是的源代码管理插件用于显示命令结果输出到与 IDE 提供的回调函数的指针。 此回调函数中将详细介绍[LPTEXTOUTPROC](../extensibility/lptextoutproc.md)。

> [!NOTE]
> 如果源代码管理插件打算利用这一点，必须已设置`SCC_CAP_TEXTOUT`中的标志[SccInitialize](../extensibility/sccinitialize-function.md)。 如果未设置该标志，或如果 IDE 不支持此功能，`lpTextOutProc`将为`NULL`。

 `dwFlags`参数控制结果的事件中打开该项目当前不存在。 它包含两个位标志`SCC_OP_CREATEIFNEW`和`SCC_OP_SILENTOPEN`。 如果存在已打开该项目，该函数只需将打开项目并返回`SCC_OK`。 如果项目不存在，并且如果`SCC_OP_CREATEIFNEW`标志为 on，源代码管理插件可以在源代码管理系统中创建项目，打开它，并返回`SCC_OK`。 如果项目不存在，并且如果`SCC_OP_CREATEIFNEW`标志处于关闭状态，该插件应然后检查`SCC_OP_SILENTOPEN`标志。 如果不在该标志，该插件可能会提示用户输入项目名称。 如果该标志上，则该插件只应返回`SCC_E_UNKNOWNPROJECT`。

## <a name="calling-order"></a>调用顺序
 中的事件，正常[SccInitialize](../extensibility/sccinitialize-function.md)将首先调用，以打开源控制会话。 会话可能包含调用`SccOpenProject`、 其他源控制插件 API 函数调用后, 跟和通过调用将终止[SccCloseProject](../extensibility/scccloseproject-function.md)。 此类会话可能会重复几次前[SccUninitialize](../extensibility/sccuninitialize-function.md)调用。

 如果源代码管理插件集`SCC_CAP_REENTRANT`位`SccInitialize`，则以上会话顺序可能会并行中重复多次。 不同`pvContext`结构跟踪不同的会话，其中，每个`pvContext`一次是与一个打开的项目相关联。 基于`pvContext`参数，该插件可以确定在任何特定的调用中引用的项目。 如果的功能位`SCC_CAP_REENTRANT`未设置，则 nonreentrant 有限的功能以使用多个项目的源代码管理插件。

> [!NOTE]
> `SCC_CAP_REENTRANT`位的源控制插件 API 版本 1.1 中引入了。 其未设置或在 1.0 版中，将被忽略，并且所有版本 1.0 源代码控制插件被都假定为 nonreentrant。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)