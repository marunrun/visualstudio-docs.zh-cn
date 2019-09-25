---
title: 编译生成
ms.date: 07/14/2017
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- builds [Visual Studio], about building in Visual Studio
- custom build steps, types of builds
ms.assetid: c7958821-285f-4e28-9e7a-b5d8b40336a1
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c99408530344c72d2e9669178c5e79f7c34d551
ms.sourcegitcommit: ea182703e922c74725045afc251bcebac305068a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71211258"
---
# <a name="compile-and-build-in-visual-studio"></a>在 Visual Studio 中编译和生成

生成源代码时，生成引擎会创建程序集和可执行应用程序。 一般情况下，生成过程在许多不同的项目类型（如 Windows、ASP.NET、移动应用和其他类型）中非常相似。 生成过程在诸如 C#、Visual Basic、C++ 和 F# 等编程语言之间也是相似的。

通过经常生成你的代码，你可以快速识别编译时错误，如不正确的语法、拼错的关键字和类型不匹配项。 还可以通过生成并运行调试版本的代码来检测和纠正运行时错误，如逻辑错误和语义错误。

成功的生成会验证应用程序的源代码是否包含正确的语法，并且是否可以解析对库、程序集和其他组件的所有静态引用。 这会生成一个应用程序可执行文件，可以在[调试环境](../debugger/index.yml)中或通过各种手动和自动的[验证代码质量](../test/improve-code-quality.md)测试来测试该可执行文件以便正常运行。 该应用程序经过完全测试后，可以编译一个发布版本以部署到客户。 要简要了解此过程，请参阅[演练：生成应用程序](../ide/walkthrough-building-an-application.md)。

可以使用以下任何方法来生成应用程序：Visual Studio IDE、MSBuild 命令行工具和 Azure Pipelines：

| 生成方法 | 优点 |
| --- |--- | --- |
| IDE |- 立即创建生成并在调试程序中对其进行测试。<br />- 运行 C++ 和 C# 项目的多处理器生成。<br />- 自定义生成系统的不同方面。 |
| MSBuild 命令行| - 在无需安装 Visual Studio 的情况下生成项目。<br />- 运行所有项目类型的多处理器生成。<br />- 自定义生成系统的大多数区域。|
| Azure Pipelines | - 自动执行生成过程作为持续集成/持续交付管道的一部分。<br />- 将自动测试应用于每个生成。<br />- 为生成过程采用几乎无限的基于云的资源。<br />- 修改生成工作流，并创建生成活动以执行深层的自定义任务。|

本节中的文档将详细介绍基于 IDE 的生成过程。 有关其他方法的详细信息，请分别参阅 [MSBuild](../msbuild/msbuild.md) 和 [Azure Pipelines](/azure/devops/pipelines/index?view=vsts)。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[在 Visual Studio for Mac 中编译和生成](/visualstudio/mac/compiling-and-building)。

## <a name="overview-of-building-from-the-ide"></a>从 IDE 生成的概述

创建项目时，Visual Studio 创建了该项目的默认生成配置和包含该项目的解决方案。  这些配置定义如何生成和部署解决方案和项目。 尤其对目标平台（如 Windows 或 Linux）和生成类型（如调试或发布）而言，项目配置必须唯一。 但是，你可以根据喜好编辑这些配置，也可以根据需要创建自己的配置。

若要初步了解如何在 IDE 中进行生成，请参阅[演练：生成应用程序](walkthrough-building-an-application.md)。

接下来，请参阅[在 Visual Studio 中生成和清理项目和解决方案](building-and-cleaning-projects-and-solutions-in-visual-studio.md)，了解你可以对过程进行哪些不同方面的自定义设置。 自定义包括[更改输出目录](how-to-change-the-build-output-directory.md)、[指定自定义生成事件](specifying-custom-build-events-in-visual-studio.md)、[管理项目依赖项](how-to-create-and-remove-project-dependencies.md)、[管理生成日志文件](how-to-view-save-and-configure-build-log-files.md)以及[禁止显示编译器警告](how-to-suppress-compiler-warnings.md)。

你还可以浏览各种其他任务：
- [了解生成配置](understanding-build-configurations.md)
- [了解生成平台](understanding-build-platforms.md)
- [管理项目和解决方案属性](managing-project-and-solution-properties.md)。
- 指定 [C#](how-to-specify-build-events-csharp.md) 和 [Visual Basic](how-to-specify-build-events-visual-basic.md) 中的生成事件。
- [设置生成选项](reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)。

## <a name="see-also"></a>请参阅

- [生成（编译）网站项目](https://msdn.microsoft.com/Library/a9cbb88c-8fff-4c67-848b-98fbfd823193)
- [编译和生成 (Visual Studio for Mac)](/visualstudio/mac/compiling-and-building)