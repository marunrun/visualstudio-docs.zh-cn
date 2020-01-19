---
title: 如何：将 Visual C++ 项目升级到 Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- projects [C++], upgrading
ms.assetid: 9a283ebb-f6d8-49c0-a73e-323979ff56a2
caps.latest.revision: 26
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: 60ba1ad7f1ed467cb1a396f80228b8915bd62a31
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918802"
---
# <a name="how-to-upgrade-visual-c-projects-to-visual-studio-2015"></a>如何：将 Visual C++ 项目升级到 Visual Studio 2015
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 2017 的最新文档，请参阅 [Visual C++ 移植和升级指南](/cpp/porting/visual-cpp-porting-and-upgrading-guide)。

当你首次打开在早期版本的 Visual Studio 中创建的 Visual C++ 项目时，系统可能会提示你更新项目。 该消息会询问你是否想要升级到 Visual C++ 编译器和库的最新版本。 升级的选项取决于用于创建该项目的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的版本。

 你可以使用 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 打开、编辑和生成在 [!INCLUDE[win8](../includes/win8-md.md)] 中创建的 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]项目，但要创建新的 [!INCLUDE[win8](../includes/win8-md.md)] 项目，你必须使用 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]。 （若要创建 [!INCLUDE[win81](../includes/win81-md.md)] 项目，必须使用 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)]。）

 若要创建 Windows 10 项目，必须使用 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]。

 如果没有提示你更新项目，则你可以不必执行任何操作来升级项目。

- 如果项目 (.vcproj) 是在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 之前的 [!INCLUDE[vs2010](../includes/vs2010-md.md)]版本中创建的，则你必须更新项目。

- 如果项目 (.vcxproj) 是在 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]、  [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]或 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 中创建的，则你有两个选择：

  - 你可以跳过更新。 如果 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] 有权访问 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] SP1、[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 或 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 中的 Visual C++ 工具，则它将加载项目而不进行任何更改。 可以通过在具有 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]的同一台计算机上安装用于创建项目的 Visual Studio 版本，来提供此访问权限 。 有关详细信息，请参阅 [Installing Visual Studio Versions Side-by-Side](../install/install-visual-studio-versions-side-by-side.md)。

  - 你可以通过允许 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 进行本主题稍后所述的更改来更新项目。 如果你的解决方案中的 Visual C++ 项目超过一个，则必须将它们全部更新。

    > [!NOTE]
    > 如果你在系统首次提醒时拒绝更新，则可以稍后在“项目”  菜单上选择“更新 VC++ 项目”  来更新项目。 如果此命令未出现，则不需要更新。

## <a name="upgrading-a-visual-c-project"></a>升级 Visual C++ 项目
 如果你允许 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] 自动更新项目，则要进行以下更改：

- 更改项目以便它使用 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] 编译器和库 (PlatformToolset = VisualStudio v140)。

- 对于 [!INCLUDE[cppcli](../includes/cppcli-md.md)] 项目，请将 TargetFrameworkVersion 更改为 .NET Framework 4.5.2。

## <a name="continuing-to-work-with-a-custom-platformtoolset"></a>继续使用自定义 PlatformToolset
 如果要继续在 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]中使用自定义的 PlatformToolset，则该工具集必须位于 x86 计算机的 %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\Platforms\Win32\PlatformToolsets\ 下，或位于 x64 计算机的 %ProgramFiles (x86)%\MSBuild\Microsoft.Cpp\v4.0\Platforms\Win32\PlatformToolsets\ 下。 有关如何创建自定义 PlatformToolset 的信息，请参见 Visual C++ 团队博客上的 [C++ 本机多目标](https://blogs.msdn.com/b/vcblog/archive/2009/12/08/c-native-multi-targeting.aspx) 。

## <a name="see-also"></a>另请参阅
 [Visual C++ 移植和升级指南](https://msdn.microsoft.com/library/f5fbcc3d-aa72-41a6-ad9a-a706af2166fb)[移植、迁移和升级 Visual Studio 项目](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)
