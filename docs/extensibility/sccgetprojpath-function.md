---
title: SccGetProjPath 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b31a17e89003967aef6a423dda87572b4a07c387
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353683"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 函数
此函数会提示用户输入项目路径，这是一个字符串，它仅对源代码管理插件有意义。 当用户是，将调用：

- 创建新的项目

- 将现有项目添加到版本控制

- 尝试查找现有的版本控制项目

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 lpUser

[in、 out]用户名 （不超过 SCC_USER_SIZE，包括 NULL 终止符）

 lpProjName

[in、 out]IDE 项目、 项目工作区中或生成文件 （不超过 SCC_PRJPATH_SIZE，包括 NULL 终止符） 的名称。

 lpLocalPath

[in、 out]项目的工作路径。 如果`bAllowChangePath`是`TRUE`，源代码管理插件可以修改此字符串 （不超过 _MAX_PATH，包括 null 终止符）。

 lpAuxProjPath

[in、 out]返回的项目路径 （不超过 SCC_PRJPATH_SIZE，包括 NULL 终止符） 的缓冲区。

 bAllowChangePath

[in]如果这是`TRUE`，可以提示和修改源代码管理插件`lpLocalPath`字符串。

 pbNew

[in、 out]传入的值指示是否创建新的项目。 返回值指示成功创建项目：

|传入|解释|
|--------------|--------------------|
|true|用户可以创建一个新的项目。|
|false|用户可能会创建一个新的项目。|

|传出|解释|
|--------------|--------------------|
|true|创建一个新的项目。|
|false|选择现有的项目。|

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功创建或检索项目。|
|SCC_I_OPERATIONCANCELED|该操作已取消。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。|
|SCC_E_CONNECTIONFAILURE|存在时尝试连接到源代码管理系统出现问题。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此函数的目的是为了 IDE 获取参数`lpProjName`和`lpAuxProjPath`。 源代码管理插件会提示用户输入此信息后，它将这两个字符串传递回 IDE。 IDE 仍然存在其解决方案文件中的这些字符串并将它们传递到[SccOpenProject](../extensibility/sccopenproject-function.md)每当用户打开此项目。 这些字符串启用该插件来跟踪与项目关联的信息。

 当首次调用该函数时，`lpAuxProjPath`设置为空字符串。 `lProjName` 也可能为空，或它可能包含源代码管理插件可能会使用或忽略的 IDE 项目名称。 该函数成功返回时，该插件返回两个相应的字符串。 IDE 不会假设即将这些字符串，不会使用它们，并将不允许用户对其进行修改。 如果用户想要更改的设置，将调用 IDE`SccGetProjPath`同样，在相同的值并向其传递以前接收了上一次。 这样，对这两个字符串插件的完全控制。

 有关`lpUser`，IDE 可能会传入用户名，或者它可能只是一个指针传递到一个空字符串。 如果用户名称，源代码管理插件应使用它作为默认值。 但是，如果未传递名称或具有给定名称的登录失败，该插件应提示用户输入的登录名和传递名称重新`lpUser`当它收到有效的登录名。 因为该插件可能会更改此字符串，IDE 会始终分配大小的缓冲区 (`SCC_USER_LEN`+ 1)。

> [!NOTE]
> IDE 将执行的第一个操作可能会调用`SccOpenProject`函数或`SccGetProjPath`函数。 因此，这两个具有相同`lpUser`参数，以使源代码管理插件在用户登录，在任一时间。 即使从函数返回表示失败，该插件必须填充此字符串与有效的登录名。

 `lpLocalPath` 是，用户将项目的目录。 它可能为空字符串。 如果没有当前定义 （如果尝试从源代码管理系统下载的项目是用户） 的目录，如果`bAllowChangePath`是`TRUE`，源代码管理插件可以提示用户输入或使用其他某种方法将其拥有字符串插入`lpLocalPath`。 如果`bAllowChangePath`是`FALSE`，该插件不应更改为字符串，因为用户已使用指定的目录中。

 如果用户创建新的项目来置于源代码管理之下，源代码管理插件可能不实际创建其源代码管理系统中时`SccGetProjPath`调用。 相反，它返回传递一个非零值的字符串沿`pbNew`，指示将源代码管理系统中创建该项目。

 例如，如果中的用户**新的项目**向导在 Visual Studio 中的将其自己的项目添加到源代码管理、 Visual Studio 会调用此函数和插件，则确定它是否可以向源代码管理系统中创建一个新项目包含 Visual Studio 项目。 如果用户单击**取消**之前完成向导，永远不会创建项目。 如果用户单击**确定**，Visual Studio 会调用`SccOpenProject`，并传入`SCC_OPT_CREATEIFNEW`，并在该时间创建受源代码管理项目。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)