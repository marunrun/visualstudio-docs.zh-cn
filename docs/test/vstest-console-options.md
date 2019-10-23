---
title: VSTest.Console.exe 命令行选项
ms.date: 07/12/2018
ms.topic: reference
helpviewer_keywords:
- vstest.console.exe
- command-line tests
ms.author: jillfra
author: jillre
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e46cd6f3589e50959ee521552bb66878147cf604
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659716"
---
# <a name="vstestconsoleexe-command-line-options"></a>VSTest.Console.exe 命令行选项

VSTest.Console.exe 是用于运行测试的命令行工具  。 可在命令行上按任意顺序指定多个选项。 这些选项在[常规命令行选项](#general-command-line-options)中列出。

> [!NOTE]
> Visual Studio 中的 MSTest 适配器在旧模式下仍有效（等效于使用 mstest.exe 运行测试），可实现兼容性  。 在旧模式下，它无法利用 TestCaseFilter 功能。 在以下情况下，适配器可以切换到旧模式：指定 .testsettings 文件、在 .runsettings 文件中将 forcelegacymode 设置为 true 或使用 HostType 等特性      。
>
> 若要在基于 ARM 架构的计算机上运行自动测试，则必须使用 VSTest.Console.exe  。

## <a name="general-command-line-options"></a>常规命令行选项

下表列出了 VSTest.Console.exe 的所有选项以及对应的简短说明  。 在命令行上键入 `VSTest.Console/?` 可以看到类似的摘要。

| 选项 | 说明 |
|---|---|
|**[测试文件]** |从指定文件运行测试。 用空格分隔多个测试文件名。<br />示例：`mytestproject.dll`、`mytestproject.dll myothertestproject.exe`|
|**/Settings:[文件名]** |使用其他设置（如数据收集器）运行测试。<br />示例：`/Settings:Local.RunSettings`|
|**/Tests:[测试名]** |运行其名称包含提供的值的测试。 若要提供多个值，请使用逗号将这些值分隔。<br />示例：`/Tests:TestMethod1,testMethod2`<br />/Tests 命令行选项不能与 /TestCaseFilter 命令行选项一起使用   。|
|**/Parallel**|指定并行执行的测试。 默认情况下，最多可使用计算机上的所有可用内核。 可在设置文件中配置要使用的内核数。|
|**/Enablecodecoverage**|在测试运行中启用数据诊断适配器 CodeCoverage。<br />如果未使用设置文件指定设置，则将使用默认设置。|
|**/InIsolation**|在隔离的进程中运行测试。<br />这种隔离使 vstest.console.exe 进程不太可能在测试出错时停止，但测试的运行速度可能较慢  。|
|**/UseVsixExtensions**|此选项使 vstest.console.exe 进程使用或跳过在测试运行中安装的 VSIX 扩展（如果有）  。<br />此选项已弃用。 从 Visual Studio 的下一个主版本开始，此选项可能会删除。 转为作为 NuGet 包提供的使用扩展。<br />示例：`/UseVsixExtensions:true`|
|**/TestAdapterPath:[路径]** |强制 vstest.console.exe 进程使用测试运行中指定路径（如果有）内的自定义测试适配器  。<br />示例：`/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[平台类型]** |将用来执行测试的目标平台体系结构。<br />有效值为 x86、x64 和 ARM。|
|**/Framework: [Framework 版本]** |要用于执行测试的目标 .NET 版本。<br />示例值有 `Framework35`、`Framework40`、`Framework45`、`FrameworkUap10`、`.NETCoreApp,Version=v1.1`。<br />如果将目标框架指定为 Framework35，则测试在 CLR 4.0“兼容模式”下运行  。<br />示例：`/Framework:framework40`|
|**/TestCaseFilter:[表达式]** |运行与给定表达式匹配的测试。<br /><Expression\> 的格式为 <property\>=<value\>[\|<Expression\>]。<br />示例：`/TestCaseFilter:"Priority=1"`<br />示例：`/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />/TestCaseFilter 命令行选项不能与 /Tests 命令行选项一起使用   。 <br />有关创建和使用表达式的信息，请参阅 [TestCase 筛选](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md)。|
|**/?**|显示使用情况信息。|
|**/Logger:[*uri/friendlyname*]**|为测试结果指定一个记录器。<br />示例：要将结果记录到 Visual Studio 测试结果文件 (TRX)，请使用 /Logger:trx  。<br />示例：要将测试结果发布到 Team Foundation Server，请使用 TfsPublisher：<br />**/logger:TfsPublisher;**<br />**Collection=<project url\>;**<br />**BuildName=<build name\>;**<br />**TeamProject=<project name\>;**<br />**[;Platform=\<Defaults to "Any CPU">]**<br />**[;Flavor=\<Defaults to "Debug">]**<br />**[;RunTitle=<title\>]**|
|**/ListTests:[文件名]** |列出给定测试容器中的已发现的测试。|
|**/ListDiscoverers**|列出已安装的测试发现器。|
|**/ListExecutors**|列出已安装的测试执行器。|
|**/ListLoggers**|列出已安装的测试记录器。|
|**/ListSettingsProviders**|列出已安装的测试设置提供程序。|
|**/Blame**|在测试执行时进行跟踪，如果测试主机进程崩溃，则按照执行顺序发出测试名称，包括崩溃发生时正在运行的特定测试。 此输出有助于轻松隔离有问题的测试并进行深入诊断。 [详细信息](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md)。|
|**/Diag:[文件名]** |将诊断跟踪日志写入指定文件。|
|**/ResultsDirectory:[*path*]**|如果不存在，则将在指定路径中创建测试结果目录。<br />示例：`/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*parentProcessId*]**|负责启动当前进程的父进程的进程 ID。|
|**/Port:[*port*]**|套接字连接和接收事件消息的端口。|
|**/Collect:[*dataCollector friendlyName*]**|为测试运行启用数据收集器。 [详细信息](https://aka.ms/vstest-collect)。|

> [!TIP]
> 选项和值不区分大小写。

## <a name="examples"></a>示例

运行 VSTest.Console.exe 的语法如下  ：

`Vstest.console.exe [TestFileNames] [Options]`

以下命令针对测试库 myTestProject.dll 运行 VSTest.Console.exe   ：

```cmd
vstest.console.exe myTestProject.dll
```

以下命令运行具有多个测试文件的 VSTest.Console.exe  。 用空格分隔测试文件名：

```cmd
Vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

以下命令运行具有多个选项的 VSTest.Console.exe  。 它在隔离进程中的 myTestFile.dll 文件中运行测试，同时使用 Local.RunSettings 文件中指定的设置   。 此外，它仅运行标记为“Priority=1”的测试，并将结果记录到 .trx 文件中  。

```cmd
vstest.console.exe  myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```
