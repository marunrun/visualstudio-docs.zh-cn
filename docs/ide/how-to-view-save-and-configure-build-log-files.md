---
title: 如何：查看、保存和配置生成日志文件 | Microsoft Docs
ms.date: 08/28/2019
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4acf8ca4e116bfb0ab990f1b0aed66bef95820ad
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283900"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>如何：查看、保存和配置生成日志文件

在 Visual Studio IDE 中生成项目之后，可以在“输出”窗口查看有关该生成的信息  。 例如，使用此信息可以排查生成失败。

- 对于 C++ 项目，还可以在生成项目时创建和保存的日志文件中查看相同的信息。 

- 对于托管的代码项目，可以单击生成输出窗口并按 Ctrl+S   。 Visual Studio 会提示你输入用于将“输出”窗口中的信息保存为日志文件的位置  。

还可以使用 IDE 指定要查看关于每个生成的信息种类。

如果使用 MSBuild 生成任何种类的项目，则可以创建日志文件来保存关于该生成的信息。 有关详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

## <a name="to-view-the-build-log-file-for-a-c-project"></a>查看 C++ 项目的生成日志文件

1. 在 Windows 资源管理器或文件资源管理器中，打开以下文件（相对于项目根文件夹）   ：Release\\<ProjectName>\>.Log* 或 Debug\\<ProjectName\>.log  

## <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>创建托管代码项目的生成日志文件

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

2. 在“输出”  窗口中，单击文本中的某个位置。

3. 按 Ctrl+S   。

   Visual Studio 会提示你输入用于保存生成输出的位置。

还可以使用 `-fileLogger` (`-fl`) 命令行选项，通过从命令行直接运行 MSBuild 来生成日志。 请参阅[用 MSBuild 获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

## <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>更改包含在生成日志中的信息量

1. 在菜单栏上，依次选择“工具” > “选项”   。

2. 在“项目和解决方案”页，选择“生成和运行”页   。

3. 在“MSBuild 项目生成输出详细信息”列表中，选择以下值之一，然后选择“确定”按钮   。

    |详细级别|描述|
    | - |-----------------|
    |**安静**|仅显示生成总结。|
    |**最低**|显示生成总结；错误、警告以及分类为极为重要的信息。|
    |**正常**|显示生成总结；错误、警告和分类为极为重要的信息；以及生成的主要步骤。 这个级别的详细信息的使用最为频繁。|
    |**详细**|显示生成总结；错误、警告和分类为极为重要的信息；生成的所有步骤；以及分类为一般重要的信息。|
    |**诊断**|显示可用于生成的所有数据。 可以使用此级别的详细信息帮助调试自定义生成脚本的问题和其他生成问题。|

     有关详细信息，请参阅[“选项”对话框->“项目和解决方案”->“生成和运行”](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)和 <xref:Microsoft.Build.Framework.LoggerVerbosity>。

    > [!IMPORTANT]
    > 要使更改在“输出”窗口（所有项目）和 \<ProjectName>.txt 文件（仅限 C++ 项目）中生效，必须重新生成该项目******。

## <a name="use-binary-logs-to-make-it-easier-to-browse-large-log-files"></a>使用二进制日志更轻松地浏览大型日志文件

二进制日志是 .NET 项目的一项可选功能，使你可以获得更丰富的日志浏览体验，从而可以更轻松地在大型日志中查找信息。 若要使用二进制日志，请安装[项目系统工具](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ProjectSystemTools)。 有关详细信息，请参阅 [https://msbuildlog.com](https://msbuildlog.com) 和[二进制日志](https://github.com/microsoft/msbuild/blob/master/documentation/wiki/Binary-Log.md)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
