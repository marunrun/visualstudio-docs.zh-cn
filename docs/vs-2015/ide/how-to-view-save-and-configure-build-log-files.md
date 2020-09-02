---
title: 如何：查看、保存和配置生成日志文件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ffc1c620136c55c42f3468129ed164075d762bff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670497"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>如何：查看、保存和配置生成日志文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio IDE 中生成项目之后，可以在“输出”窗口查看有关该生成的信息  。 例如，使用此信息可以排查生成失败。 对于 C++ 项目，还可以在某个自动创建和保存的 .txt 文件中查看相同的信息。 对于托管代码项目，可以从“输出”窗口中将信息复制粘贴到 .txt 文件中，然后自行保存****。 还可以使用 IDE 指定要查看关于每个生成的信息种类。

 如果使用 MSBuild 生成任何种类的项目，则可以创建 .txt 文件来保存关于该生成的信息。 有关详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

### <a name="to-view-the-build-log-file-for-a-c-project"></a>查看 C++ 项目的生成日志文件

1. 在“Windows 资源管理器”或“文件资源管理器”中，打开以下文件：\\...\Visual Studio Version\Projects\\ProjectName\\ProjectName\Debug\\ProjectName.txt****************

### <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>创建托管代码项目的生成日志文件

1. 在菜单栏上，依次选择 **“生成”**、 **“生成解决方案”**。

2. 在“输出”窗口，突出显示来自生成的信息，然后将其复制到剪贴板****。

3. 打开文本编辑器（如记事本），将信息粘贴到该文件中，然后保存。

### <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>更改包含在生成日志中的信息量

1. 在菜单栏上，依次选择 " **工具**"、" **选项**"。

2. 在“项目和解决方案”页，选择“生成和运行”页   。

3. 在“MSBuild 项目生成输出详细信息”列表中，选择以下值之一，然后选择“确定”按钮   。

    |详细级别|说明|
    |---------------------|-----------------|
    |无提示|仅显示生成总结。|
    |最低|显示生成总结；错误、警告以及分类为极为重要的信息。|
    |普通|显示生成总结；错误、警告和分类为极为重要的信息；以及生成的主要步骤。 这个级别的详细信息的使用最为频繁。|
    |详细|显示生成总结；错误、警告和分类为极为重要的信息；生成的所有步骤；以及分类为一般重要的信息。|
    |诊断|显示可用于生成的所有数据。 可以使用此级别的详细信息帮助调试自定义生成脚本的问题和其他生成问题。|

     有关详细信息，请参阅 " [选项" 对话框、项目和解决方案、生成并运行](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md) 和 <xref:Microsoft.Build.Framework.LoggerVerbosity> 。

    > [!IMPORTANT]
    > 您必须重新生成项目，以使所做的更改在 " **输出** " 窗口中生效 (所有项目) 和项目 *名称*.Txt 文件 (c + + 项目仅) 。

## <a name="see-also"></a>另请参阅
 [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)[编译和生成](../ide/compiling-and-building-in-visual-studio.md)
