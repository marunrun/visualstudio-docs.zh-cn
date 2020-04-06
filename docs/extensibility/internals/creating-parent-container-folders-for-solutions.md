---
title: 为解决方案创建父容器文件夹 |微软文档
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
ms.openlocfilehash: 3e5481e20a12fc05ccba97eef55173e5ce9b30d6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709099"
---
# <a name="create-parent-container-folders-for-solutions"></a>为解决方案创建父容器文件夹
在源代码管理插件 API 版本 1.2 中，用户可以为解决方案中的所有 Web 项目指定单个根源控制目标。 此单个根称为超级统一根 （SUR）。

 在源代码管理插件 API 版本 1.1 中，如果用户向源代码管理添加了多项目解决方案，系统将提示用户为每个 Web 项目指定一个源代码管理目标。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新函数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理添加解决方案时，IDE 几乎总是创建 SUR 文件夹。 具体而言，它在以下情况下这样做：

- 该项目是文件共享 Web 项目。

- 项目和解决方案文件有不同的驱动器。

- 项目和解决方案文件有不同的共享。

- 项目单独添加（在源代码管理的解决方案中）。

在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，建议 SUR 文件夹的名称与没有扩展的解决方案名称相同。 下表总结了两个版本中的行为。

|Feature|源代码管理插件 API 版本 1.1|源代码管理插件 API 版本 1.2|
|-------------| - | - |
|将解决方案添加到 SCC|分初始化（）<br /><br /> SccGetProjPath（）<br /><br /> SccGetProjPath（）<br /><br /> SccOpen项目（）|分初始化（）<br /><br /> SccGetProjPath（）<br /><br /> Scccreate 子项目（）<br /><br /> Scccreate 子项目（）<br /><br /> SccOpen项目（）|
|将项目添加到源控制的解决方案|SccGetProjPath（）<br /><br /> 打开项目（）|SccGet家长项目路径（）<br /><br /> SccOpen项目（）<br /><br />  **注：** 可视化工作室假定解决方案是 SUR 的直接子级。|

## <a name="examples"></a>示例
 下表列出了两个示例。 在这两种情况下，都会[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提示用户在源代码管理下为解决方案指定目标位置，直到*将user_choice*指定为目标。 指定user_choice时，将添加解决方案和两个项目，而不提示用户进行源代码管理目标。

|解决方案包含|磁盘位置|数据库默认结构|
|-----------------------|-----------------------|--------------------------------|
|*sln1.sln*<br /><br /> Web1<br /><br /> Web2|*C：\解决方案\sln1*<br /><br /> *C：[Inetpub]wwwroot_Web1*<br /><br /> \\[服务器]wwwroot$_Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1.sln*<br /><br /> Web1<br /><br /> 赢1|*C：\解决方案\sln1*<br /><br /> *D：[Inetpub]wwwroot_Web1*<br /><br /> *C：\解决方案\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 无论操作是由于错误而取消还是失败，都会创建 SUR 文件夹和子文件夹。 它们不会在取消或错误条件下自动删除。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]如果源代码管理插件不返回`SCC_CAP_CREATESUBPROJECT`并且`SCC_CAP_GETPARENTPROJECT`功能标志，则默认为版本 1.1 行为。 此外，用户[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可以选择通过将以下键的值设置为*dword：0000001*来还原到版本 1.1 行为：

 **[HKEY_CURRENT_USER_软件\微软[VisualStudio]8.0\源控制]不创建解决方案 RootfolderinSourceControl** = *dword：0000001*

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
