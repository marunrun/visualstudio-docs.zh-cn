---
title: 为解决方案创建父级容器文件夹 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d50800e527c6e79100bf699172f7fc30881b3299
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332732"
---
# <a name="create-parent-container-folders-for-solutions"></a>创建父容器的解决方案文件夹
在源控制插件 API 版本 1.2，用户可以指定一个根源控制目标的解决方案中的所有 web 项目。 此单个根称为超级统一根 (SUR)。

 在源控件插件 API 版本 1.1 中，如果将用户添加到源代码管理的多项目解决方案已提示用户指定的每个 web 项目的一个源控制目标。

## <a name="new-capability-flags"></a>新的功能标志
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新的函数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时将解决方案添加到源代码管理后，IDE 将几乎总是创建 SUR 文件夹。 具体而言，它是在以下情况下：

- 项目是一个文件共享 web 项目。

- 有不同的项目和解决方案文件的驱动器。

- 没有为项目和解决方案文件的不同共享。

- 将项目添加单独 （在受源代码管理解决方案）。

在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，建议 SUR 文件夹的名称是不带扩展名的解决方案名称相同。 下表总结了两个版本中的行为。

|功能|源代码管理插件 API 版本 1.1|源代码管理插件 API 版本 1.2|
|-------------| - | - |
|将解决方案添加到源代码管理|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccGetProjPath()<br /><br /> SccOpenProject()|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject()|
|将项目添加到受源代码管理解决方案|SccGetProjPath()<br /><br /> OpenProject()|SccGetParentProjectPath()<br /><br /> SccOpenProject()<br /><br />  **注意：** Visual Studio 假设一种解决方案是 SUR.的直接子级|

## <a name="examples"></a>示例
 下表列出了两个示例。 在这两种情况下，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]会提示用户输入到源代码管理下的解决方案的目标位置*user_choice*指定为目标。 当指定 user_choice 时，而不提示用户输入源控制目标添加解决方案和两个项目。

|解决方案包含|有关磁盘位置|数据库默认结构|
|-----------------------|-----------------------|--------------------------------|
|*sln1.sln*<br /><br /> Web1<br /><br /> Web2|*C:\Solutions\sln1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot$\Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1.sln*<br /><br /> Web1<br /><br /> Win1|*C:\Solutions\sln1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 无论该操作已取消或因出错而失败创建 SUR 文件夹和子文件夹。 它们不会自动删除在取消或错误状态。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如果源代码管理插件不会返回默认为版本 1.1 行为`SCC_CAP_CREATESUBPROJECT`和`SCC_CAP_GETPARENTPROJECT`功能标志。 此外，用户的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可以选择将以下键的值设置还原到版本 1.1 行为*dword: 00000001*:

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl** = *dword:00000001*

## <a name="see-also"></a>请参阅
- [什么是源控制插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)