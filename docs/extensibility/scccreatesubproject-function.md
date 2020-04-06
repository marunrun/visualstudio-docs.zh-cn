---
title: Scccreate 子项目功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74354e05b16830f599dd706fbe48aadd75b11a18
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701041"
---
# <a name="scccreatesubproject-function"></a>SccCreate 子项目功能
此函数在参数指定的现有父项目下创建具有给定名称的`lpParentProjPath`子项目。

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

[在]源代码管理插件上下文指针。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpUser

[进出]用户名（最多SCC_USER_SIZE，包括 NULL 终止符）。

 lpParentProjPath

[在]标识父项目的路径的字符串（最多SCC_PRJPATH_SIZE，包括 NULL 终止符）。

 lpSubProj名称

[在]建议的子项目名称（最多SCC_PRJPATH_SIZE，包括 NULL 终止符）。

 lpAuxProjPath

[进出]标识项目的辅助字符串（最多SCC_PRJPATH_SIZE，包括 NULL 终止符）。

 lpSubProjPath

[进出]标识子项目的路径的输出字符串（最多SCC_PRJPATH_SIZE，包括 NULL 终止符）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功创建子项目。|
|SCC_E_INITIALIZEFAILED|无法初始化父项目。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|无法创建子项目。|
|SCC_E_PROJSYNTAXERR|无效的项目语法。|
|SCC_E_UNKNOWNPROJECT|源控件插件未知父项目。|
|SCC_E_INVALIDFILEPATH|无效或无法使用的文件路径。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_CONNECTIONFAILURE|存在源代码管理插件连接问题。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特异性故障。|

## <a name="remarks"></a>备注
 如果已存在名称的子项目，则函数可以更改默认名称以创建唯一名称，例如向其中添加"#\<数字>"。 调用方必须准备好接受 对`lpUser`的`lpSubProjPath`更改。 `lpAuxProjPath` 然后`lpSubProjPath`，`lpAuxProjPath`在调用[SccOpenProject](../extensibility/sccopenproject-function.md)中使用 和 参数。 调用方不应在返回时修改它们。 这些字符串为源代码管理插件提供了一种跟踪它需要与项目关联的信息的方法。 调用方 IDE 在返回时不会显示这两个参数，因为插件可以使用可能不适合查看的格式化字符串。 函数返回成功或失败代码，如果成功，则用新项目的完整项目路径填充`lpSubProjPath`变量。

 此函数类似于[SccGetProjPath，](../extensibility/sccgetprojpath-function.md)只不过它默默地创建一个项目，而不是提示用户选择一个项目。 调用函数`SccCreateSubProject`时，`lpParentProjName``lpAuxProjPath`不会为空，并且将对应于有效的项目。 这些字符串通常由 IDE 从以前对`SccGetProjPath`函数的调用或[SccGet 父项目路径](../extensibility/sccgetparentprojectpath-function.md)接收。

 参数`lpUser`是用户名。 IDE 将传递以前从 接收`SccGetProjPath`的相同用户名，源代码管理插件应使用该名称作为默认值。 如果用户已与插件建立了打开的连接，则插件应尝试消除任何提示，以确保该函数静默工作。 但是，如果登录失败，插件应提示用户登录，并在收到有效的登录时，将名称转回`lpUser`。 由于插件可能会更改此字符串，因此 IDE 将始终分配大小缓冲区（SCC_USER_LEN+1 或SCC_USER_SIZE，其中包括空终止符的空间）。 如果更改了字符串，则新字符串必须是有效的登录名（至少与旧字符串一样有效）。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>用于 SccCreate 子项目和 SccGet 父项目路径的技术说明
 在 Visual Studio 中，将解决方案和项目添加到源代码管理中已简化，以最大程度地减少提示用户选择源代码管理系统中位置的次数。 如果源代码管理插件同时支持新功能和`SccCreateSubProject``SccGetParentProjectPath`，则 Visual Studio 将激活这些更改。 但是，以下注册表项可用于禁用这些更改并恢复到以前的 Visual Studio（源代码管理插件 API 版本 1.1）行为：

 **[HKEY_CURRENT_USER_软件\微软[VisualStudio]8.0\源控制]"不创建解决方案 RootfolderinSourceControl"=dword：0000001**

 如果此注册表项不存在或设置为 dword：00000000，Visual Studio 将尝试使用新功能和`SccCreateSubProject``SccGetParentProjectPath`。

 如果注册表项设置为 dword：00000001，Visual Studio 不会尝试使用这些新功能，并且添加到源代码管理的操作将像在 Visual Studio 的早期版本中那样工作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
