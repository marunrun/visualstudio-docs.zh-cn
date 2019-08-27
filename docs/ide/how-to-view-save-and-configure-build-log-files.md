---
title: 如何：查看、保存和配置生成日志文件 | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0dc172723005b6781a63b3a3956b12152d73bb0f
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415579"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>如何：查看、保存和配置生成日志文件

在 Visual Studio IDE 中生成项目之后，可以在“输出”窗口查看有关该生成的信息  。 例如，使用此信息可以排查生成失败。 

- 对于 C++ 项目，还可以在某个自动创建和保存的 .txt 文件中查看相同的信息  。 

- 对于托管的代码项目，可以单击生成输出窗口并按 Ctrl+S   。 Visual Studio 会提示你输入用于将“输出”  窗口中的信息保存为 .txt  文件的位置。 

还可以使用 IDE 指定要查看关于每个生成的信息种类。

如果使用 MSBuild 生成任何种类的项目，则可以创建 .txt 文件来保存关于该生成的信息  。 有关详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

## <a name="to-view-the-build-log-file-for-a-c-project"></a>查看 C++ 项目的生成日志文件

1. 在“Windows 资源管理器”或“文件资源管理器”中，打开以下文件：\\...\Visual Studio \<Version\>\Projects\\<ProjectName\>\\<ProjectName\>\Debug\\<ProjectName\>.txt   

## <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>创建托管代码项目的生成日志文件

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

2. 在“输出”  窗口中，单击文本中的某个位置。

3. 按 Ctrl+S   。

   Visual Studio 会提示你输入用于保存生成输出的位置。

## <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>更改包含在生成日志中的信息量

1. 在菜单栏上，依次选择“工具” > “选项”   。

2. 在“项目和解决方案”页，选择“生成和运行”页   。

3. 在“MSBuild 项目生成输出详细信息”列表中，选择以下值之一，然后选择“确定”按钮   。

    |详细级别|说明|
    | - |-----------------|
    |**安静**|仅显示生成总结。|
    |**最低**|显示生成总结；错误、警告以及分类为极为重要的信息。|
    |**正常**|显示生成总结；错误、警告和分类为极为重要的信息；以及生成的主要步骤。 这个级别的详细信息的使用最为频繁。|
    |**详细**|显示生成总结；错误、警告和分类为极为重要的信息；生成的所有步骤；以及分类为一般重要的信息。|
    |**诊断**|显示可用于生成的所有数据。 可以使用此级别的详细信息帮助调试自定义生成脚本的问题和其他生成问题。|

     有关详细信息，请参阅[“选项”对话框->“项目和解决方案”->“生成和运行”](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)和 <xref:Microsoft.Build.Framework.LoggerVerbosity>。

    > [!IMPORTANT]
    > 更改要在“输出”窗口（所有项目）和 \<ProjectName>.txt 文件（仅限 C++ 项目）中生效，必须重新生成该项目   。

## <a name="see-also"></a>请参阅

- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)
- [在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
