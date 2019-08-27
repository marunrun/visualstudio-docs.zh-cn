---
title: Devenv 命令行开关
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- switches, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db9aaeb48095b058abb0deefa342598eefeed1b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970216"
---
# <a name="devenv-command-line-switches"></a>Devenv 命令行开关

借助 Devenv，可以设置关于 IDE、生成项目、调试项目和使用命令行部署项目的各种选项。 使用这些开关，可以通过脚本或 .bat 文件（如每日构建版脚本）运行 IDE，也可以特定配置启动 IDE。

> [!NOTE]
> 对于与生成相关的任务，建议使用 MSBuild，而不是 devenv。 有关详细信息，请参阅 [MSBuild 命令行参考](../../msbuild/msbuild-command-line-reference.md)。

若要了解与 VSPackage 开发相关的开关，另请参阅[适用于 VSPackage 开发的 Devenv 命令行开关](../../extensibility/devenv-command-line-switches-for-vspackage-development.md)。

## <a name="devenv-switch-syntax"></a>Devenv 开关语法

以 `devenv` 开头的命令由 `devenv.com` 实用程序处理，该实用程序通过标准系统流（例如 `stdout` 和 `stderr`）提供输出。 该实用工具在捕获输出时（例如输出到 .txt 文件）确定相应的 I/O 重定向。

或者，以 `devenv.exe` 开头的命令可以使用相同的开关，但会绕过 `devenv.com` 实用工具。 直接使用 `devenv.exe` 可阻止输出出现在控制台上。

`devenv` 开关的语法规则与其他 DOS 命令行实用工具的规则类似。 下列语法规则适用于所有 `devenv` 开关及其参数：

- 命令以 `devenv` 开头。

- 开关不区分大小写。

- 可使用连字符 (-) 或正斜杠 (/) 来指定开关。

- 指定一个解决方案或项目时，第一个参数是解决方案文件或项目文件的名称，包括文件路径。

- 如果第一个参数是不属于解决方案或项目的文件，此文件在相应编辑器的 IDE 新实例中打开。

- 如果提供项目文件名而不是解决方案文件名，`devenv` 命令会在项目文件的父文件夹中搜索具有相同名称的解决方案文件。 例如，`devenv myproject1.vbproj /build` 命令在父文件夹中搜索命名为“`myproject1.sln`”的解决方案文件。

  > [!NOTE]
  > 引用此项目的唯一一个解决方案文件应位于其父文件夹中。 如果父文件夹不包含引用此项目的解决方案文件，或父文件夹包含引用此项目的两个或更多解决方案文件，将创建一个临时解决方案文件。

- 当文件路径和文件名中包含空格时，必须用引号 ("") 将它们括起来。 例如 `"c:\project a\"`。

- 在同一行上的开关和参数之间插入一个空白字符。 例如，`devenv /log output.txt` 命令打开 IDE，并将相应会话的所有日志信息都输出到 output.txt 中。

- 无法在 `devenv` 命令中使用模式匹配语法。

## <a name="devenv-switches"></a>Devenv 开关

下面各个命令行开关显示 IDE，并执行所描述的任务。

|命令行开关|说明|
| - |-----------------|
|[/Command](command-devenv-exe.md)|启动 IDE 并执行指定的命令。<br /><br /> `devenv /command "nav https://docs.microsoft.com/"`|
|[/DebugExe](debugexe-devenv-exe.md)|在调试器的控制下加载 C++ 可执行文件。 此开关不适用于 Visual Basic 或 C# 可执行文件。 有关详细信息，请参阅[自动启动调试器中的进程](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger)。<br /><br /> `devenv /debugexe mysln.exe`|
|[/Diff](diff.md)|比较两个文件。 采用四个参数：SourceFile、TargetFile、SourceDisplayName（可选）和 TargetDisplayName（可选）。<br /><br /> `devenv /diff File1 File2 Alias1 Alias2`|
|[/DoNotLoadProjects](donotloadprojects-devenv-exe.md)|打开指定的解决方案，而不加载任何项目。<br /><br /> `devenv /donotloadprojects mysln.sln`|
|[/Edit](edit-devenv-exe.md)|在此应用程序的运行实例中打开指定的文件。 如果没有正在运行的实例，它启动具有简化的窗口布局的新实例。<br /><br /> `devenv /edit File1 File2`|
|[/LCID 或 /L](lcid-devenv-exe.md)|为 IDE 设置默认语言。 如果 Visual Studio 安装中不包括指定语言，此设置遭忽略。<br /><br /> `devenv /l 1033`|
|[/Log](log-devenv-exe.md)|启动 Visual Studio 并将所有活动记录到日志文件中。<br /><br /> `devenv /log mylogfile.xml`|
|[/NoSplash](nosplash-devenv-exe.md)|打开 IDE，而不显示初始屏幕。<br /><br /> `devenv /nosplash File1 File2`|
|[/Run 或 /R](run-devenv-exe.md)|编译并运行指定的解决方案。<br /><br /> `devenv /run mysln.sln`|
|[/RunExit](runexit-devenv-exe.md)|编译并运行指定的解决方案，在运行该解决方案时最小化 IDE，并在解决方案完成运行后关闭 IDE。<br /><br /> `devenv /runexit mysln.sln`|
|[/SafeMode](safemode-devenv-exe.md)|在安全模式下启动 Visual Studio。 此开关仅加载默认环境、默认服务以及第三方包的发布版。<br /><br /> 此开关不带参数。|
|[/UseEnv](useenv-devenv-exe.md)|让 IDE 使用 PATH、INCLUDE、LIBPATH 和 LIB 环境变量，以用于 C++ 编译。 此开关与使用 C++ 的桌面开发工作负载一起安装。 有关更多信息，请参阅 [为命令行生成设置路径和环境变量](/cpp/build/setting-the-path-and-environment-variables-for-command-line-builds)。|

下面各个命令行开关不显示 IDE。

|命令行开关|说明|
| - |-----------------|
|[/?](q-devenv-exe.md)|在“命令提示符”窗口中显示 `devenv` 开关的相关帮助信息。<br /><br /> 此开关不带参数。|
|[build](build-devenv-exe.md)|根据指定解决方案的配置，生成指定的解决方案或项目。<br /><br /> `devenv mysln.sln /build`|
|[/Clean](clean-devenv-exe.md)|删除由生成命令创建的任何文件，而不影响源文件。<br /><br /> `devenv mysln.sln /clean`|
|[/Deploy](deploy-devenv-exe.md)|根据解决方案的配置，生成解决方案以及部署所需的文件。<br /><br /> `devenv mysln.sln /deploy`|
|[/Out](out-devenv-exe.md)|用于在生成时指定一个文件来接收错误。<br /><br /> `devenv mysln.sln /build Debug /out log.txt`|
|[/Project](project-devenv-exe.md)|要生成、清理或部署的项目。 仅当已提供 `/Build`、`/Rebuild`、`/Clean` 或 `/Deploy` 开关之后，才可使用此开关。<br /><br /> `devenv mysln.sln /build Debug /project proj1`|
|[/ProjectConfig](projectconfig-devenv-exe.md)|指定要生成或部署的项目配置。 仅当已提供 `/Project` 开关之后，才可使用此开关。<br /><br /> `devenv mysln.sln /build Release /project proj1 /projectconfig Release`|
|[/Rebuild](rebuild-devenv-exe.md)|根据指定解决方案的配置，清理并生成指定的解决方案或项目。<br /><br /> `devenv mysln.sln /rebuild`|
|[/ResetSettings](resetsettings-devenv-exe.md)|还原 Visual Studio 默认设置。 可视需要将这些设置重置为指定的 `.vssettings` 文件。<br /><br /> `devenv /resetsettings mysettings.vssettings`|
|[/Upgrade](upgrade-devenv-exe.md)|将指定的解决方案文件及其所有项目文件或指定的项目文件升级为这些文件的当前 Visual Studio 格式。<br /><br /> `devenv mysln.sln /upgrade`|

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](general-environment-options-dialog-box.md)
- [适用于 VSPackage 开发的 Devenv 命令行开关](../../extensibility/devenv-command-line-switches-for-vspackage-development.md)
