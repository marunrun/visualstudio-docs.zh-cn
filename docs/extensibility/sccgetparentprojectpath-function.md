---
title: SccGetParentProjectPath 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f258558207f86ff76746d18aa432fe4c5850290
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700715"
---
# <a name="sccgetparentprojectpath-function"></a>SccGetParentProjectPath 函数
此函数确定指定项目的父项目路径。 当用户将 Visual Studio 项目添加到源代码管理中时，将调用此函数。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetParentProjectPath(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpProjPath,
   LPSTR  lpAuxProjPath,
   LPSTR  lpParentProjPath
);
```

### <a name="parameters"></a>参数
 pContext

中源代码管理插件上下文指针。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpUser

[in，out]用户名最多 (SCC_USER_SIZE，包括 NULL 终止符) 。

 lpProjPath

中标识项目路径的字符串，最多 (SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpAuxProjPath

[in，out]标识项目的辅助字符串 (最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpParentProjPath

[in，out]标识父项目路径的输出字符串 (最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功获取父项目路径。|
|SCC_E_INITIALIZEFAILED|项目无法初始化。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理插件。|
|SCC_E_UNKNOWNPROJECT|项目对于源代码管理插件是未知的。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_CONNECTIONFAILURE|存储连接问题。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数返回成功或失败代码，如果成功，则 `lpParentProjPath` 使用指定项目的完整项目路径填充该变量。

 此函数返回现有项目的父项目路径。 对于根项目，函数将返回传入的项目路径 (即) 的相同根项目路径。 请注意，项目路径是一个仅对源代码管理插件有意义的字符串。

 IDE 已准备好接受对 `lpUser` 和参数的更改 `lpAuxProjPath` 。 当用户在将来打开此项目时，IDE 将保留这些字符串并将其传递给 [SccOpenProject](../extensibility/sccopenproject-function.md) 。 因此，这些字符串为源代码管理插件提供了一种跟踪与项目关联的信息所需的方法。

 此函数类似于 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)，只不过它不会提示用户选择一个项目。 它也不会创建新项目，但仅适用于现有项目。

 在 `SccGetParentProjectPath` 调用时， `lpProjPath` 和 `lpAuxProjPath` 将不为空，并且将对应于有效的项目。 IDE 通常会从以前对函数的调用接收这些字符串 `SccGetProjPath` 。

 `lpUser`参数为用户名。 IDE 将传入之前从函数接收的相同用户名 `SccGetProjPath` ，并且源代码管理插件应使用该名称作为默认名称。 如果用户已与插件建立了打开的连接，则该插件应尝试消除任何提示，以确保函数无提示地工作。 但是，如果登录失败，则插件应提示用户输入登录名，并在收到有效的登录名后，将该名称传回 `lpUser` 。 因为插件可能会更改此字符串，所以 IDE 将始终 (+ 1) 分配大小的缓冲区 `SCC_USER_LEN` 。 如果更改了字符串，则新字符串必须是有效的登录名， (至少与旧字符串) 有效。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject 和 SccGetParentProjectPath 的技术说明
 在 Visual Studio 中，将解决方案和项目添加到源代码管理已得到简化，以最大程度地减少在源代码管理系统中提示用户选择位置的次数。 如果源代码管理插件支持两个新函数（ [SccCreateSubProject](../extensibility/scccreatesubproject-function.md) 和函数），则 Visual Studio 会激活这些更改 `SccGetParentProjectPath` 。 但是，可以使用以下注册表项来禁用这些更改，并恢复到以前的 Visual Studio (源代码管理插件 API 版本 1.1) 行为：

 **[HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl" = dword：00000001**

 如果此注册表项不存在或设置为 dword：00000000，则 Visual Studio 将尝试使用新的函数 `SccCreateSubProject` 和 `SccGetParentProjectPath` 。

 如果注册表项设置为 dword：00000001，则 Visual Studio 不会尝试使用这些新函数，并且添加到源代码管理中的操作的工作方式与 Visual Studio 早期版本中的工作方式相同。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
