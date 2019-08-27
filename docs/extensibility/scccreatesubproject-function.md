---
title: SccCreateSubProject 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8aa70f6b42a6722ac66340807503ee4494795b0d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327520"
---
# <a name="scccreatesubproject-function"></a>SccCreateSubProject 函数
此函数具有给定名称指定现有父项目下创建子项目`lpParentProjPath`参数。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCreateSubProject(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpParentProjPath,
   LPCSTR lpSubProjName,
   LPSTR  lpAuxProjPath,
   LPSTR  lpSubProjPath
);
```

### <a name="parameters"></a>参数
 pContext

[in]源控件插件上下文指针。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 lpUser

[in、 out]（最多 SCC_USER_SIZE，包括 NULL 终止符) 用户名。

 lpParentProjPath

[in]标识父项目 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 的路径的字符串。

 lpSubProjName

[in]建议的子项目名称 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符)。

 lpAuxProjPath

[in、 out]标识 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 项目的辅助字符串。

 lpSubProjPath

[in、 out]标识 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 的子项目的路径的输出字符串。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功创建子项目。|
|SCC_E_INITIALIZEFAILED|无法初始化父项目。|
|SCC_E_INVALIDUSER|用户不可以登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|不能创建子项目。|
|SCC_E_PROJSYNTAXERR|无效的项目的语法。|
|SCC_E_UNKNOWNPROJECT|父项目是未知的源代码管理插件。|
|SCC_E_INVALIDFILEPATH|无效或不可用的文件路径。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_CONNECTIONFAILURE|出现源控制插件的连接问题。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 如果已存在同名的子项目，该函数可以更改默认名称创建一个唯一的活动，例如通过添加"_\<数 >"到它。 调用方必须准备好接受将变为`lpUser`， `lpSubProjPath`，和`lpAuxProjPath`。 `lpSubProjPath`并`lpAuxProjPath`然后在调用中使用参数[SccOpenProject](../extensibility/sccopenproject-function.md)。 它们不应在返回调用方修改。 这些字符串提供一种方法的源代码管理插件来跟踪需要与项目关联的信息。 调用方 IDE 不会显示在返回时，这两个参数，因为该插件可以使用可能适于查看的格式化的字符串。 该函数将返回成功或失败的代码，并且如果成功，填充变量`lpSubProjPath`替换为新项目的完整项目路径。

 此函数是类似于[SccGetProjPath](../extensibility/sccgetprojpath-function.md)，只不过它将以无提示方式创建一个项目，而不是提示用户选择一个。 当`SccCreateSubProject`调用函数时，`lpParentProjName`和`lpAuxProjPath`不为空，并且将对应于有效的项目。 这些字符串通常由在 IDE 的以前调用接收`SccGetProjPath`函数或[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)。

 `lpUser`参数是用户名称。 IDE 将传入它必须从以前接收的相同用户名称`SccGetProjPath`，和源代码管理插件应使用的默认名称。 如果用户已使用该插件的打开连接，然后该插件应尝试消除任何提示，确保该函数以静默方式工作。 但是，如果登录失败，该插件应提示用户的登录名中，并且当它收到有效的登录名，名称重新的传递`lpUser`。 因为该插件可能会更改此字符串，IDE 将始终分配的缓冲区大小 （SCC_USER_LEN + 1 或 SCC_USER_SIZE，其中包括 null 终止符的占用空间）。 如果字符串已更改，新的字符串必须是有效的登录名 （至少为有效的旧字符串作为）。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject 和 SccGetParentProjectPath 的技术说明
 将解决方案和项目添加到源代码管理中简化了 Visual Studio 以最大程度减少系统会提示用户选择源代码管理系统中的位置的次数。 如果源代码管理插件支持两个新函数，这些更改激活由 Visual Studio`SccCreateSubProject`和`SccGetParentProjectPath`。 但是，可以使用以下注册表项来禁用这些更改并还原到以前的 Visual Studio (源控制插件 API 版本 1.1) 行为：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl"=dword:00000001**

 如果此注册表项不存在，或设置为 dword:00000000，Visual Studio 将尝试使用新函数`SccCreateSubProject`和`SccGetParentProjectPath`。

 如果注册表项设置为 dword: 00000001，Visual Studio 不会尝试使用这些新函数，并将添加到源代码管理的操作起来就像在早期版本的 Visual Studio 中那样。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)