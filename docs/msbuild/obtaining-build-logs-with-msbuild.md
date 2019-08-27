---
title: 用 MSBuild 获取生成日志 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, logging
- logging [MSBuild]
ms.assetid: 6ba9a754-9cc0-4fed-9fc8-4dcd3926a031
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 385871a47b2a4d73a1f7afacf9d39a02d7c782ca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963762"
---
# <a name="obtain-build-logs-with-msbuild"></a>用 MSBuild 获取生成日志

使用 MSBuild 开关，可指定要查看的生成数据量，以及是否要将生成数据保存到一个或多个文件。 还可指定一个自定义记录器来收集生成数据。 对于本主题未涉及的 MSBuild 命令行开关的相关信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。

> [!NOTE]
> 如果使用 Visual Studio IDE 生成项目，则可通过查看生成日志排除这些生成中的故障。 有关详细信息，请参阅[如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。

## <a name="set-the-level-of-detail"></a>设置详细信息级别

 在不指定详细信息等级的情况下使用 MSBuild 生成项目时，输出日志中会出现以下信息：

- 错误、警告和被分类为极为重要的消息。

- 一些状态事件。

- 生成总结。

使用 -verbosity (-v) 开关，可控制输出日志中的数据量。 对于故障排除，请使用 `detailed` (`d`) 或 `diagnostic` (`diag`) 的详细级别，它可提供大部分信息。

如果你将 -verbosity 设置为 `detailed`，生成流程可能会减速；如果你将 -verbosity 设置为 `diagnostic`，此流程甚至会更慢。

```cmd
msbuild MyProject.proj -t:go -v:diag
```

### <a name="verbosity-settings"></a>详细级别设置

下表显示日志详细级别（列值）如何影响记录的消息类型（行值）。

|                                       | Quiet | 最低 | 普通 | 详细 | 诊断 |
|---------------------------------------|:-----:|:-------:|:------:|:--------:|:----------:|
| 错误                                |   ✅   |    ✅    |    ✅   |     ✅    |      ✅     |
| 警告                              |   ✅   |    ✅    |    ✅   |     ✅    |      ✅     |
| 高重要性消息              |       |    ✅    |    ✅   |     ✅    |      ✅     |
| 一般重要性消息           |       |         |    ✅   |     ✅    |      ✅     |
| 低重要性消息              |       |         |        |     ✅    |      ✅     |
| 其他 MSBuild 引擎信息 |       |         |        |          |      ✅     |

## <a name="save-the-build-log-to-a-file"></a>将生成日志保存到文件中

可使用 -fileLogger (fl) 开关，将生成数据保存到文件中。 以下示例将生成数据保存到名为“msbuild.log”的文件。

```cmd
msbuild MyProject.proj -t:go -fileLogger
```

 在以下示例中，日志文件被命名为“MyProjectOutput.log”，且日志输出的详细级别设置为了 `diagnostic`。 使用 -filelogparameters (`flp`) 开关指定这两个设置。

```cmd
msbuild MyProject.proj -t:go -fl -flp:logfile=MyProjectOutput.log;verbosity=diagnostic
```

 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。

## <a name="save-the-log-output-to-multiple-files"></a>将日志输出保存到多个文件中

 以下示例将整个日志保存到了 msbuild1.log，将错误保存到了 JustErrors.log，并且将警告保存到了 JustWarnings.log。 该示例为三个文件中的每个文件都使用了文件编号。 文件编号是紧跟在 -fl 和 -flp 开关后面指定（例如，`-fl1` 和 `-flp1`）。

 文件 2 和 3 的 -filelogparameters (`flp`) 开关指定了每个文件的名称和内容。 未为文件 1 指定名称，因此使用了默认名称“msbuild1.log”。

```cmd
msbuild MyProject.proj -t:go -fl1 -fl2 -fl3 -flp2:logfile=JustErrors.log;errorsonly -flp3:logfile=JustWarnings.log;warningsonly
```

 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。

## <a name="save-a-binary-log"></a>保存二进制日志

可使用 -binaryLogger (bl) 开关，以压缩二进制格式保存日志。 此日志包含生成进程的详细说明，并可以由某些日志分析工具读取。

在以下示例中，创建了名为“binarylogfilename”的二进制日志文件。

```cmd
-bl:binarylogfilename.binlog
```

有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)。

## <a name="use-a-custom-logger"></a>使用自定义记录器

 可以通过创作一个实现 <xref:Microsoft.Build.Framework.ILogger> 接口的托管类型来编写自己的记录器。 例如，可使用自定义记录程序，在电子邮件中发送生成错误，将其记录到数据库，或记录到 XML 文件。 有关详细信息，请参阅[生成记录器](../msbuild/build-loggers.md)。

 在 MSBuild 命令行中，可使用 -logger 开关指定自定义记录器。 还可使用 -noconsolelogger 开关，禁用默认控制台记录器。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.Build.Framework.LoggerVerbosity>
- [生成记录器](../msbuild/build-loggers.md)
- [多处理器环境下的日志记录](../msbuild/logging-in-a-multi-processor-environment.md)
- [创建转发记录器](../msbuild/creating-forwarding-loggers.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)