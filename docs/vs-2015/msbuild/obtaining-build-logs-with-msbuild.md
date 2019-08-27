---
title: 用 MSBuild 获取生成日志 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, logging
- logging [MSBuild]
ms.assetid: 6ba9a754-9cc0-4fed-9fc8-4dcd3926a031
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c88288a7bed453ca14e9c14fd43706b97be04044
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430849"
---
# <a name="obtaining-build-logs-with-msbuild"></a>用 MSBuild 获取生成日志
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 MSBuild 开关，可指定要查看的生成数据量，以及是否要将生成数据保存到一个或多个文件。 还可指定一个自定义记录器来收集生成数据。 对于本主题未涉及的 MSBuild 命令行开关的相关信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。  
  
> [!NOTE]
> 如果使用 Visual Studio IDE 生成项目，则可通过查看生成日志排除这些生成中的故障。 有关详细信息，请参阅[如何：查看、 保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。  
  
## <a name="setting-the-level-of-detail"></a>设置详细信息级别  
 在不指定详细信息等级的情况下使用 MSBuild 生成项目时，输出日志中会出现以下信息：  
  
- 错误、警告和被分类为极为重要的消息。  
  
- 一些状态事件。  
  
- 生成总结。  
  
  使用 **/verbosity** (**/v**) 开关可控制出现在输出日志中的数据量。 对于故障排除，请使用 `detailed` (`d`) 或 `diagnostic` (`diag`) 的详细级别，它可提供大部分信息。  
  
  将 **/verbosity** 设置为 `detailed` 时，生成过程会减慢；将 **/verbosity** 设置为 `diagnostic` 时，该过程会更慢。  
  
```  
msbuild MyProject.proj /t:go /v:diag  
```  
  
## <a name="saving-the-build-log-to-a-file"></a>将生成日志保存到文件中  
 可使用 **/fileLogger** (**fl**) 开关将生成数据保存到文件。 以下示例将生成数据保存到名为 `msbuild.log` 的文件。  
  
```  
msbuild MyProject.proj /t:go /fileLogger  
```  
  
 在以下示例中，日志文件被命名为 `MyProjectOutput.log`，且日志输出的详细级别设置为了 `diagnostic`。 使用 **/filelogparameters** (`flp`) 开关可指定这两个设置。  
  
```  
msbuild MyProject.proj /t:go /fl /flp:logfile=MyProjectOutput.log;verbosity=diagnostic  
```  
  
 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。  
  
## <a name="saving-the-log-output-to-multiple-files"></a>将日志输出保存到多个文件中  
 以下示例将整个日志保存到了 `msbuild1.log`，将错误保存到了 `JustErrors.log`，并且将警告保存到了 `JustWarnings.log`。 该示例为三个文件中的每个文件都使用了文件编号。 在 **/fl** 和 **/flp** 开关（例如， `/fl1` 和 `/flp1`）后指定了文件编号。  
  
 文件 2 和 3 的 **/Filelogparameters** (`flp`) 开关指定每个文件的名称及文件内容。 未为文件 1 指定名称，因此使用了默认名称 `msbuild1.log`。  
  
```  
msbuild MyProject.proj /t:go /fl1 /fl2 /fl3 /flp2:logfile=JustErrors.log;errorsonly /flp3:logfile=JustWarnings.log;warningsonly  
  
```  
  
 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。  
  
## <a name="using-a-custom-logger"></a>使用自定义记录器  
 可以通过创作一个实现 <xref:Microsoft.Build.Framework.ILogger> 接口的托管类型来编写自己的记录器。 例如，可使用自定义记录程序，在电子邮件中发送生成错误，将其记录到数据库，或记录到 XML 文件。 有关详细信息，请参阅[生成记录器](../msbuild/build-loggers.md)。  
  
 在 MSBuild 命令行中，可使用 **/logger** 开关指定自定义记录器。 还可使用 **/noconsolelogger** 开关禁用默认控制台记录器。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.Build.Framework.LoggerVerbosity>   
 [生成记录器](../msbuild/build-loggers.md)   
 [多处理器环境下的日志记录](../msbuild/logging-in-a-multi-processor-environment.md)   
 [创建转发记录器](../msbuild/creating-forwarding-loggers.md)   
 [MSBuild 概念](../msbuild/msbuild-concepts.md)
