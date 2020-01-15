---
title: 生成和清理项目和解决方案
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
f1_keywords:
- VS.BuildProjectPicker
- vs.batchbuild
helpviewer_keywords:
- Clean Solution command
- builds [Visual Studio], managing
- solution build configurations, starting
- Build Solution command
- project build configurations, starting
- build configurations, starting
- project build configurations, dependencies
- Rebuild Solution command
- solution build configurations, build order
- builds [Visual Studio], preparing
ms.assetid: 710891fd-379e-42c2-a84b-44a7af694ca0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f3e71fe9b6179ac8f7ac69b0cb987fdbc30459fb
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596523"
---
# <a name="build-and-clean-projects-and-solutions-in-visual-studio"></a>在 Visual Studio 中生成和清理项目和解决方案

通过本主题中的过程，学会生成、重新生成或清除解决方案中的所有/部分项目/项目项。 有关分步教程，请参阅[演练：生成应用程序](../ide/walkthrough-building-an-application.md)。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[在 Visual Studio for Mac 中生成和清除项目和解决方案](/visualstudio/mac/building-and-cleaning-projects-and-solutions)。

> [!NOTE]
> 你的 Visual Studio 版本中的 UI 可能与此主题中描述的有所不同，具体取决于现用的设置。 若要更改设置，例如“常规”或“Visual C++”设置，请选择“工具” > “导入和导出设置”，再选择“重置所有设置”      。

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>生成、重新生成或清理整个解决方案

1. 在“解决方案资源管理器”  中，选择或打开解决方案。

2. 在菜单栏上选择“生成”  ，然后选择下列命令之一：

    - 选择“生成”  或“生成解决方案”  ，仅编译自最近生成以来更改过的项目文件和组件。

        > [!NOTE]
        > 当解决方案包括多个项目时，“生成”  命令将变成“生成解决方案”  。

    - 选择“重新生成解决方案”  清理解决方案，然后创建所有项目文件和组件。

    - 选择“清理解决方案”  ，删除任何中间文件和输出文件。 仅剩下项目和组件文件后，可生成中间文件和输出文件的新实例。

## <a name="to-build-or-rebuild-a-single-project"></a>生成或重新生成单个项目

1. 在“解决方案资源管理器”  中，选择或打开项目。

2. 在菜单栏上选择“生成”  ，然后选择“生成”  “ProjectName”  或“重新生成”  “ProjectName”  。

    - 选择“生成”  “ProjectName”  可仅生成自最近生成以来更改过的项目组件。

    - 选择“重新生成“  ”ProjectName”  可以“清理”项目，然后生成项目文件和所有项目组件。

## <a name="to-build-only-the-startup-project-and-its-dependencies"></a>仅生成启动项目及其依赖项

1. 在菜单栏上，依次选择“工具” > “选项”   。

2. 在“选项”  对话框框中，展开“项目和解决方案”  节点，然后选择“生成和运行”  页。

     “生成和运行” > “项目和解决方案” > “选项”对话框随即打开    。

3. 选择“在运行时仅生成启动项目和依赖项”  复选框。

     选中此复选框后，执行以下步骤之一时，将仅生成当前启动项目及其依赖项：

    - 在菜单栏上，依次选择“调试” > “启动”(F5)    。

    - 在菜单栏上，依次选择“生成” > “生成解决方案”(Ctrl+Shift+B)      。

    清理此复选框后，运行以上任一命令时，会生成所有项目、项目依赖项和解决方案文件。 默认情况下清除此复选框。

## <a name="to-build-only-the-selected-visual-c-project"></a>仅生成选定的 Visual C++ 项目

选择 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 项目，然后在菜单栏上选择“生成” > “仅项目”，再选择下列某个命令   ：

- 仅生成  ProjectName 

- 仅重新生成  ProjectName 

- 仅清理  ProjectName 

- 仅链接  ProjectName 

这些命令仅适用于所选的 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 项目，而不会生成、重新生成、清理或链接任何项目依赖项或解决方案文件。 根据 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的版本，“仅项目”  子菜单可能包含更多命令。

## <a name="to-compile-multiple-c-project-items"></a>编译多个 C++ 项目项

在“解决方案资源管理器”  中，选择多个具有可编译操作的文件，打开某个文件的快捷菜单，然后选择“编译”  。

如果文件具有依赖项，则按依赖顺序编译文件。 如果编译时无法提供文件所需的预编译标头，编译操作将失败。 编译操作使用当前的活动解决方案配置。

## <a name="to-stop-a-build"></a>停止生成

任意执行以下步骤之一：

- 在菜单栏上，选择“生成” > “取消”   。

- 按 Ctrl +Break   。

## <a name="see-also"></a>请参阅

- [如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)
- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [了解生成配置](../ide/understanding-build-configurations.md)
- [如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)
- [C/C++ 生成参考](/cpp/build/reference/c-cpp-building-reference)
- [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
- [解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)
- [生成和清除项目和解决方案 (Visual Studio for Mac)](/visualstudio/mac/building-and-cleaning-projects-and-solutions)
