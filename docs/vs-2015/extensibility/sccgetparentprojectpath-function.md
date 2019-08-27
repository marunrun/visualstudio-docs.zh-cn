---
title: SccGetParentProjectPath 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a631936dee7608306edfcd86f686b788e57133f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200085"
---
# <a name="sccgetparentprojectpath-function"></a>SccGetParentProjectPath 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数将确定指定的项目的父项目路径。 用户将 Visual Studio 项目添加到源代码管理时，调用此函数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccGetParentProjectPath(  
   LPVOID pContext,  
   HWND   hWnd,  
   LPSTR  lpUser,  
   LPCSTR lpProjPath,  
   LPSTR  lpAuxProjPath,  
   LPSTR  lpParentProjPath  
);  
```  
  
#### <a name="parameters"></a>参数  
 pContext  
 [in]源控件插件上下文指针。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 lpUser  
 [in、 out]（最多 SCC_USER_SIZE，包括 NULL 终止符) 的用户名。  
  
 lpProjPath  
 [in]标识 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 的项目路径的字符串。  
  
 lpAuxProjPath  
 [in、 out]标识 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 项目的辅助字符串。  
  
 lpParentProjPath  
 [in、 out]标识父项目路径 （最多 SCC_PRJPATH_SIZE，包括 NULL 终止符) 的输出字符串。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|成功地获取父项目路径。|  
|SCC_E_INITIALIZEFAILED|无法初始化项目。|  
|SCC_E_INVALIDUSER|用户不可以登录到源代码管理插件。|  
|SCC_E_UNKNOWNPROJECT|项目是未知的源代码管理插件。|  
|SCC_E_INVALIDFILEPATH|无效或不可用的文件路径。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_PROJSYNTAXERR|无效的项目的语法。|  
|SCC_E_CONNECTIONFAILURE|存储连接时出现问题。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 此函数将返回成功或失败的代码，以及如果成功，填充变量`lpParentProjPath`替换为指定的项目的完整项目路径。  
  
 此函数返回父级的现有项目的项目路径。 对于根项目中，函数将返回传入的项目路径 （即，同一个根项目路径）。 请注意，项目路径仅对源代码管理插件有意义的字符串。  
  
 IDE 已准备好接受对更改`lpUser`和`lpAuxProjPath`以及参数。 IDE 将保留这些字符串并将它们传递给[SccOpenProject](../extensibility/sccopenproject-function.md)用户在将来打开此项目时。 这些字符串，因此，提供一种方法进行源代码管理插件，它需要将与项目关联的跟踪信息。  
  
 此函数是类似于[SccGetProjPath](../extensibility/sccgetprojpath-function.md)，只不过它不会提示用户选择一个项目。 它也永远不会仅与一个现有项目创建一个新的项目，但工作原理。  
  
 当`SccGetParentProjectPath`调用时，`lpProjPath`和`lpAuxProjPath`不为空，并且将对应于有效的项目。 这些字符串通常由在 IDE 的以前调用接收`SccGetProjPath`函数。  
  
 `lpUser`参数是用户名称。 IDE 将传入它必须从以前接收的相同用户名称`SccGetProjPath`函数和源代码管理插件应使用名称作为默认值。 如果用户已使用该插件的打开连接，然后该插件应尝试消除任何提示，确保该函数以静默方式工作。 但是，如果登录失败，该插件应提示用户的登录名中，并且当它收到有效的登录名，名称重新的传递`lpUser`。 因为该插件可能会更改此字符串，IDE 会始终分配大小的缓冲区 (`SCC_USER_LEN`+ 1)。 如果字符串已更改，新的字符串必须是有效的登录名 （至少为有效的旧字符串作为）。  
  
## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject 和 SccGetParentProjectPath 的技术说明  
 将解决方案和项目添加到源代码管理中简化了 Visual Studio 以最大程度减少系统会提示用户选择源代码管理系统中的位置的次数。 如果源代码管理插件支持两个新函数，这些更改激活由 Visual Studio [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)和`SccGetParentProjectPath`函数。 但是，可以使用以下注册表项来禁用这些更改并还原到以前的 Visual Studio (源控制插件 API 版本 1.1) 行为：  
  
 [HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl"= dword: 00000001  
  
 如果此注册表项不存在，或设置为 dword:00000000，Visual Studio 将尝试使用新函数`SccCreateSubProject`和`SccGetParentProjectPath`。  
  
 如果注册表项设置为 dword: 00000001，Visual Studio 不会尝试使用这些新函数，并将添加到源代码管理的操作起来就像在早期版本的 Visual Studio 中那样。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)   
 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
