---
title: SccGetProjPath 功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700695"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 功能
此函数提示用户输入项目路径，这是一个仅对源代码管理插件有意义的字符串。 当用户为：

- 创建新项目

- 将现有项目添加到版本控制

- 尝试查找现有版本控制项目

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpUser

[进出]用户名（不超过SCC_USER_SIZE，包括 NULL 终止符）

 lpProjName

[进出]IDE 项目、项目工作区或 makefile 的名称（不超过SCC_PRJPATH_SIZE，包括 NULL 终止符）。

 lp本地路径

[进出]项目的工作路径。 如果是`bAllowChangePath``TRUE`，源代码管理插件可以修改此字符串（不超过_MAX_PATH，包括空终止符）。

 lpAuxProjPath

[进出]返回的项目路径的缓冲区（不超过SCC_PRJPATH_SIZE，包括 NULL 终止符）。

 bAllow改变路径

[在]如果是`TRUE`，源代码管理插件可以提示和修改`lpLocalPath`字符串。

 pb 新

[进出]中的值表示是否创建新项目。 返回的值表示创建项目的成功：

|传入|解释|
|--------------|--------------------|
|TRUE|用户可以创建新项目。|
|FALSE|用户可能无法创建新项目。|

|传出|解释|
|--------------|--------------------|
|TRUE|创建了一个新项目。|
|FALSE|已选择现有项目。|

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功创建或检索项目。|
|SCC_I_OPERATIONCANCELED|已经取消了操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。|
|SCC_E_CONNECTIONFAILURE|尝试连接到源代码管理系统时出现问题。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此函数的目的是使 IDE 获取参数`lpProjName`和`lpAuxProjPath`。 在源代码管理插件提示用户获取此信息后，它将这两个字符串传回 IDE。 IDE 将这些字符串保留在其解决方案文件中，并在用户打开此项目时将其传递到[SccOpenProject。](../extensibility/sccopenproject-function.md) 这些字符串使插件能够跟踪与项目关联的信息。

 首次调用函数时，`lpAuxProjPath`将设置为空字符串。 `lProjName`也可能为空，或者可能包含 IDE 项目名称，源代码管理插件可能使用或忽略该名称。 当函数成功返回时，插件将返回两个相应的字符串。 IDE 不对这些字符串进行假设，不会使用它们，也不会允许用户修改它们。 如果用户想要更改设置，IDE 将再次调用`SccGetProjPath`，传递与上次接收的相同值。 这使插件能够完全控制这两个字符串。

 对于`lpUser`，IDE 可能会传递用户名，也可以简单地将指针传递到空字符串。 如果存在用户名，源代码管理插件应将其用作默认值。 但是，如果未传递任何名称，或者登录失败与给定的名称，插件应提示用户登录，并在收到有效的登录时将名称传回`lpUser`。 由于插件可能会更改此字符串，因此 IDE 将始终分配大小缓冲区 （+1）。`SCC_USER_LEN`

> [!NOTE]
> IDE 执行的第一个操作可能是对`SccOpenProject`函数或函数的`SccGetProjPath`调用。 因此，它们都有相同的`lpUser`参数，这使得源代码管理插件可以在任一时间登录用户。 即使从函数返回指示失败，插件也必须用有效的登录名填充此字符串。

 `lpLocalPath`是用户保存项目的目录。 它可能是一个空字符串。 如果当前没有定义目录（例如，用户尝试从源代码管理系统下载项目），如果是`bAllowChangePath``TRUE`，源代码管理插件可以提示用户输入或使用其他方法将其自己的字符串放入 。 `lpLocalPath` 如果是`bAllowChangePath``FALSE`，插件不应更改字符串，因为用户已在指定的目录中工作。

 如果用户创建新项目以置于源代码管理之下，则在调用源代码`SccGetProjPath`管理系统中，源代码管理插件实际上可能不会创建它。 相反，它将字符串与 的非`pbNew`零值一起传递，指示将在源代码管理系统中创建项目。

 例如，如果 Visual Studio 中的 **"新项目**"向导中的用户将项目添加到源代码管理中，Visual Studio 将调用此函数，该插件确定是否可以在源代码管理系统中创建新项目以包含 Visual Studio 项目。 如果用户在完成向导之前单击 **"取消"，** 则永远不会创建项目。 如果用户单击 **"确定**"，则此时将调用`SccOpenProject`Visual `SCC_OPT_CREATEIFNEW`Studio 传入 ，并创建源控制的项目。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
