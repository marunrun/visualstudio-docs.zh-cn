---
title: 正在为解决方案创建父容器文件夹 |Microsoft Docs
description: 了解如何使用源代码管理插件 API 版本1.2 为解决方案中的所有 web 项目指定一个根源代码管理目标。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e65da2b50984b0259079a1693dd31d400e1e12e3
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96329934"
---
# <a name="create-parent-container-folders-for-solutions"></a>为解决方案创建父容器文件夹
在源代码管理插件 API 版本1.2 中，用户可以为解决方案中的所有 web 项目指定一个根源代码管理目标。 此单个根称为超级统一根 (.SUR) 。

 在源代码管理插件 API 版本1.1 中，如果用户将多项目解决方案添加到源代码管理，则系统会提示用户为每个 web 项目指定一个源代码管理目标。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新函数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在将解决方案添加到源代码管理中时，IDE 几乎始终会创建 .sur 文件夹。 具体而言，在以下情况下，它会执行此操作：

- 项目是文件共享 web 项目。

- 项目和解决方案文件存在不同的驱动器。

- 项目和解决方案文件存在不同的共享。

- 项目是在源代码管理的解决方案) 中单独添加的 (。

在中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，建议 .sur 文件夹的名称与不带扩展名的解决方案名称相同。 下表总结了两个版本中的行为。

|功能|源代码管理插件 API 版本1。1|源代码管理插件 API 版本1。2|
|-------------| - | - |
|将解决方案添加到 SCC|SccInitialize ( # A1<br /><br /> SccGetProjPath ( # A1<br /><br /> SccGetProjPath ( # A1<br /><br /> SccOpenProject ( # A1|SccInitialize ( # A1<br /><br /> SccGetProjPath ( # A1<br /><br /> SccCreateSubProject ( # A1<br /><br /> SccCreateSubProject ( # A1<br /><br /> SccOpenProject ( # A1|
|将项目添加到源代码管理的解决方案|SccGetProjPath ( # A1<br /><br /> OpenProject ( # A1|SccGetParentProjectPath ( # A1<br /><br /> SccOpenProject ( # A1<br /><br />  **注意：**  Visual Studio 假定解决方案是 .SUR 的直接子级。|

## <a name="examples"></a>示例
 下表列出了两个示例。 在这两种情况下， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 系统都会提示用户在源代码管理下输入解决方案的目标位置，直到将  *user_choice* 指定为目标。 当指定 user_choice 时，将添加解决方案和两个项目，而不提示用户提供源代码管理目标。

|解决方案包含|磁盘位置上|数据库默认结构|
|-----------------------|-----------------------|--------------------------------|
|*sln1 .sln*<br /><br /> Web1<br /><br /> Web2|*C:\Solutions\sln1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot $ \Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1 .sln*<br /><br /> Web1<br /><br /> Win1|*C:\Solutions\sln1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 不管操作被取消还是因错误而失败，都将创建 .SUR 文件夹和子文件夹。 它们不会在取消或错误情况中自动删除。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如果源代码管理插件未返回 `SCC_CAP_CREATESUBPROJECT` 并且功能标志，则默认为版本1.1 行为 `SCC_CAP_GETPARENTPROJECT` 。 此外，用户 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可以通过将以下项的值设置为 *dword*，选择恢复到1.1 版本：00000001：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl**  = *dword： 00000001*

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
