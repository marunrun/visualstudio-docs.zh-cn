---
title: SccOpenProject 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fbf566e593bb1ddbc31c70de1570d746a14fbdcf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700573"
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

[in，out]用户的名称不能超过 SCC_USER_SIZE （包括 NULL 终止符) ） (。

 lpProjName

中标识项目名称的字符串。

 lpLocalProjPath

中项目的工作文件夹的路径。

 lpAuxProjPath

[in，out]标识项目的可选辅助字符串 (不能超过 SCC_AUXPATH_SIZE （包括 NULL 终止符) ）。

 lpComment

中为正在创建的新项目添加注释。

 lpTextOutProc

中用于显示源代码管理插件文本输出的可选回调函数。

 dwFlags 

中指示当项目对于源代码管理插件未知时是否需要创建一个新项目。 值可以是和的组合 `SCC_OP_CREATEIFNEW``SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|打开项目成功。|
|SCC_E_INITIALIZEFAILED|项目无法初始化。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|在调用之前，该项目不存在; `SCC_OPT_CREATEIFNEW` 已设置该标志，但无法创建该项目。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_UNKNOWNPROJECT|项目对于源代码管理插件是未知的， `SCC_OPT_CREATEIFNEW` 未设置该标志。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECFICERROR|不特定的失败;源代码管理系统未初始化。|

## <a name="remarks"></a>备注
 IDE 可能会传入用户名 (`lpUser`) ，或者它可能只是传入指向空字符串的指针。 如果存在用户名，则源代码管理插件应该使用该用户名作为默认值。 但是，如果未传递任何名称，或者如果登录失败，则该插件应该提示用户登录，并将在收到有效的登录名时返回有效的名称， `lpUser` `.` 因为插件可能会更改用户名字符串，而 IDE 将始终分配大小 `SCC_USER_LEN` 为 (+ 1 或 SCC_USER_SIZE 的缓冲区，这包括用于空终止符) 的空间。

> [!NOTE]
> IDE 可能需要执行的第一个操作可能是对 `SccOpenProject` 函数或 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)的调用。 出于此原因，它们都具有相同的 `lpUser` 参数。

 `lpAuxProjPath` 和从 `lpProjName` 解决方案文件中读取，或从对函数的调用返回 `SccGetProjPath` 。 这些参数包含源代码管理插件与项目关联的字符串，仅对插件有意义。 如果解决方案文件中不存在此类字符串，并且未提示用户浏览 (这会通过函数) 返回一个字符串 `SccGetProjPath` ，则 IDE 会传递和的空字符串 `lpAuxProjPath` `lpProjName` ，并且在此函数返回时，这些值将被插件更新。

 `lpTextOutProc` 是一个指针，指向用于显示命令结果输出的 IDE 为源代码管理插件提供的回调函数。 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)中详细介绍了此回调函数。

> [!NOTE]
> 如果源代码管理插件打算利用此方法，则必须 `SCC_CAP_TEXTOUT` 在 [SccInitialize](../extensibility/sccinitialize-function.md)中设置标志。 如果未设置该标志，或者如果 IDE 不支持此功能， `lpTextOutProc` 则将为 `NULL` 。

 `dwFlags`参数控制正在打开的项目当前不存在的结果。 它由两个 bitflags （ `SCC_OP_CREATEIFNEW` 和）组成 `SCC_OP_SILENTOPEN` 。 如果要打开的项目已存在，则该函数只会打开项目并返回 `SCC_OK` 。 如果项目不存在并且 `SCC_OP_CREATEIFNEW` 标志为 on，则源代码管理插件可以在源代码管理系统中创建项目，打开该项目，然后返回 `SCC_OK` 。 如果该项目不存在，并且 `SCC_OP_CREATEIFNEW` 标志为 off，则该插件随后应检查 `SCC_OP_SILENTOPEN` 标志。 如果该标志未打开，则插件可能会提示用户输入项目名称。 如果该标志已打开，则该插件只应返回 `SCC_E_UNKNOWNPROJECT` 。

## <a name="calling-order"></a>调用顺序
 在正常事件的过程中，将首先调用 [SccInitialize](../extensibility/sccinitialize-function.md) 以打开源代码管理会话。 会话可能包含对的调用 `SccOpenProject` ，后跟其他源代码管理插件 API 函数调用，并将通过调用 [SccCloseProject](../extensibility/scccloseproject-function.md)而终止。 此类会话可能会在调用 [SccUninitialize](../extensibility/sccuninitialize-function.md) 之前重复多次。

 如果源代码管理插件在 `SCC_CAP_REENTRANT` 中设置位 `SccInitialize` ，则上述会话序列可能会并行重复多次。 不同的 `pvContext` 结构跟踪不同的会话，其中每个会话 `pvContext` 一次与一个打开的项目相关联。 `pvContext`插件可以基于参数确定在任何特定调用中引用的项目。 如果 `SCC_CAP_REENTRANT` 未设置功能位，则 nonreentrant 源代码管理插件在处理多个项目的能力方面受到限制。

> [!NOTE]
> 该 `SCC_CAP_REENTRANT` 位是在源代码管理插件 API 版本1.1 中引入的。 在版本1.0 中未设置或已忽略，并且假定所有版本1.0 源代码管理插件都是 nonreentrant。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
