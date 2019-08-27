---
title: 编译和生成
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- builds [Visual Studio], about building in Visual Studio
- custom build steps, types of builds
ms.assetid: c7958821-285f-4e28-9e7a-b5d8b40336a1
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b534e46f4cdef87641207ec13419d4c59d04ed3f
ms.sourcegitcommit: b56dc6fadc6c924beed36bb4c2ccc16cf6bcfa1c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2019
ms.locfileid: "68740079"
---
# <a name="compiling-and-building-in-visual-studio"></a>在 Visual Studio 中编译和生成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在开发周期中，您可以使用 Visual Studio 频繁生成应用程序和创建程序集和可执行程序。 通过经常生成您的代码，您可以更早地标识编译时错误，如不正确的语法、拼错的关键字和类型不匹配项。 您还可以通过频繁生成并运行调试版本的代码来检测和纠正运行时错误，如逻辑错误和语义错误。

 在完全开发和充分调试项目或解决方案之后，您可以在发行版中编译其组件。 默认情况下，发行版将进行优化，并且设计为比调试版本更小且运行速度更快。 有关详细信息，请参见[演练：生成应用程序](../ide/walkthrough-building-an-application.md)。

## <a name="choosing-a-build-method"></a>选择一种生成方法
 您可以在命令提示符处使用 IDE 中的默认生成选项或使用 Team Foundation Build 来生成应用程序。 其中的每个选项都将 MSBuild 用作基础技术，并且每种方法都有特定的好处，如下表所示。

|生成方法|优点|更多相关信息|
|------------------|--------------|--------------------------|
|使用 IDE|-   可以更轻松地创建并立即运行生成。<br />-   可以运行 C++ 和 C# 项目的多处理器生成。<br />-   可以自定义生成系统的某些方面。|[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)|
|运行 MSBuild 命令行|-   可以生成项目，而无需安装 Visual Studio。<br />-   可以运行所有项目类型的多处理器生成。<br />-   可以自定义生成系统的大多数区域。|[MSBuild](../msbuild/msbuild.md)|
|使用 Team Foundation Build|-   可以将生成过程自动化。 例如，您可以在夜间或每次签入此代码时生成一个或多个项目。 还可以在共享的生成服务器而不是开发计算机上生成项目。<br />-   可以快速指定要生成的代码、要运行的测试和其他常用选项。<br />-   可以修改生成工作流，并根据需要创建生成活动以执行深层的自定义任务。|[生成应用程序](/azure/devops/pipelines/index)|

## <a name="building-from-the-ide"></a>从 IDE 生成
 创建一个项目时，将为此项目定义默认生成配置，并为其分配解决方案生成配置以便为生成提供上下文。 解决方案配置定义如何生成和部署解决方案中的项目。 项目配置是一组项目属性，这些属性对于平台和生成类型是唯一的（例如，Release Win32）。 您可以编辑这些默认配置，并且可以创建您自己的配置。 有关详细信息, 请参阅[项目设计器简介](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)和[笔尖如何:修改项目属性和配置设置](https://msdn.microsoft.com/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)。

 从 IDE 中，你可以执行以下额外任务：

- [更改生成输出目录](../ide/how-to-change-the-build-output-directory.md)。

- [标识依赖于另一个项目中的输出的项目以便正确生成](../ide/how-to-create-and-remove-project-dependencies.md)。

- [更改包含在生成日志或生成的“输出”窗口中的信息量](../ide/how-to-view-save-and-configure-build-log-files.md)。

- [隐藏 Visual C#、Visual C++ 或 Visual Basic 的特定编译器警告](../ide/how-to-suppress-compiler-warnings.md)。

- [为生成指定自定义预编译和编译后操作](../ide/specifying-custom-build-events-in-visual-studio.md)。

- 通过使用并行生成改进生成性能。 有关详细信息，请参阅[并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)或博客文章 [Tuning C++ build parallelism](http://blogs.msdn.com/b/msbuild/archive/2010/03/08/tuning-c-build-parallelism-in-vs2010.aspx)（调整 C++ 并行生成）。

## <a name="see-also"></a>请参阅
 [演练：构建应用程序](../ide/walkthrough-building-an-application.md) [了解生成配置](../ide/understanding-build-configurations.md)[了解生成平台](../ide/understanding-build-platforms.md)生成[(编译) 网站项目](https://msdn.microsoft.com/library/a9cbb88c-8fff-4c67-848b-98fbfd823193) [如何:创建和删除项目依赖项](../ide/how-to-create-and-remove-project-dependencies.md)
