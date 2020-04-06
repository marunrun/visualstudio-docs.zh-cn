---
title: SccOpen项目功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700573"
---
# <a name="sccopenproject-function"></a>SccOpenProject 函数
此函数将打开现有源代码管理项目或创建新的源代码管理项目。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpUser

[进出]用户的名称（不超过SCC_USER_SIZE，包括 NULL 终止符）。

 lpProjName

[在]标识项目名称的字符串。

 lpLocalProjPath

[在]项目工作文件夹的路径。

 lpAuxProjPath

[进出]标识项目的可选辅助字符串（不超过SCC_AUXPATH_SIZE，包括 NULL 终止符）。

 lpComment

[在]注释正在创建的新项目。

 lpTextOutProc

[在]用于显示源控件插件的文本输出的可选回调功能。

 dwFlags

[在]如果源控制插件不知道项目，则指示是否需要创建新项目。 值可以是`SCC_OP_CREATEIFNEW`和`SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功打开项目。|
|SCC_E_INITIALIZEFAILED|无法初始化项目。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|项目在调用之前不存在;因此，该项目在调用之前不存在。 已`SCC_OPT_CREATEIFNEW`设置标志，但无法创建项目。|
|SCC_E_PROJSYNTAXERR|无效的项目语法。|
|SCC_E_UNKNOWNPROJECT|源控件插件不知道该项目，`SCC_OPT_CREATEIFNEW`并且未设置标志。|
|SCC_E_INVALIDFILEPATH|无效或无法使用的文件路径。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECFICERROR|非特异性故障;源控制系统未初始化。|

## <a name="remarks"></a>备注
 IDE 可能传递用户名 （`lpUser`），也可以简单地将指针传递到空字符串。 如果存在用户名，源代码管理插件应将其用作默认值。 但是，如果未传递名称，或者登录失败，并且给定名称失败，插件应提示用户登录，并在收到有效登录`lpUser``.`时返回有效名称，因为插件可能会更改用户名字符串，IDE 将始终分配大小缓冲区（+1`SCC_USER_LEN`或SCC_USER_SIZE，其中包括空终止符的空间）。

> [!NOTE]
> IDE 可能需要执行的第一个操作可能是对`SccOpenProject`函数或[SccGetProjPath](../extensibility/sccgetprojpath-function.md)的调用。 因此，它们都有相同的`lpUser`参数。

 `lpAuxProjPath`并从`lpProjName`解决方案文件中读取，或者从调用函数`SccGetProjPath`返回它们。 这些参数包含源代码管理插件与项目关联字符串，并且仅对插件有意义。 如果解决方案文件中没有此类字符串，并且未提示用户浏览（这将通过`SccGetProjPath`函数返回字符串），则 IDE 将传递 和`lpAuxProjPath``lpProjName`的空字符串，并期望此函数返回时插件会更新这些值。

 `lpTextOutProc`是 IDE 为显示命令结果输出而向源代码管理插件提供的回调函数的指针。 此回调函数在[LPTEXTOUTPROC 中](../extensibility/lptextoutproc.md)进行了详细介绍。

> [!NOTE]
> 如果源代码管理插件打算利用这一点，它必须在[Scc 初始化](../extensibility/sccinitialize-function.md)中`SCC_CAP_TEXTOUT`设置了标志。 如果未设置该标志，或者 IDE 不支持此功能，`lpTextOutProc`则将为`NULL`。

 如果`dwFlags`当前未打开的项目不存在，参数将控制结果。 它由两个位标志`SCC_OP_CREATEIFNEW`和`SCC_OP_SILENTOPEN`组成。 如果打开的项目已存在，则函数只需打开项目并返回`SCC_OK`。 如果项目不存在，并且`SCC_OP_CREATEIFNEW`标志处于打开状态，源代码管理插件可以在源代码管理系统中创建项目，打开它，然后返回`SCC_OK`。 如果项目不存在，并且`SCC_OP_CREATEIFNEW`标志已关闭，则插件应检查该`SCC_OP_SILENTOPEN`标志。 如果该标志未打开，插件可能会提示用户输入项目名称。 如果该标志处于打开，插件应仅返回`SCC_E_UNKNOWNPROJECT`。

## <a name="calling-order"></a>调用订单
 在正常事件过程中，将首先调用[Scc 初始化](../extensibility/sccinitialize-function.md)以打开源代码管理会话。 会话可以包含对 的`SccOpenProject`调用，然后是其他源代码管理插件 API 函数调用，并且将随着对[SccCloseProject](../extensibility/scccloseproject-function.md)的调用而终止。 在调用[SccUn初始化](../extensibility/sccuninitialize-function.md)之前，可以重复多次此类会话。

 如果源代码管理插件将`SCC_CAP_REENTRANT`位设置在`SccInitialize`中，则上述会话序列可能会并行重复多次。 不同的`pvContext`结构跟踪不同的会话，其中每个`pvContext`会话一次与一个打开的项目相关联。 根据参数`pvContext`，插件可以确定任何特定调用中引用哪个项目。 如果未设置功能位`SCC_CAP_REENTRANT`，则非重新进入源控制插件处理多个项目的能力受到限制。

> [!NOTE]
> 该`SCC_CAP_REENTRANT`位是在源代码管理插件 API 的 1.1 版中引入的。 它在版本 1.0 中未设置或被忽略，并且所有版本 1.0 源代码管理插件都假定为非重新进入。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
