---
title: Devenv 命令行开关 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- switches, Devenv
- builds [Team System], command-line
- applications [Visual Studio], executing
- compiling source code, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
- environment, Devenv commands
- compilers, Devenv commands
- switches
- Devenv, syntax and list of switches
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b8b0683024e2881f76bb6c54d9420d351fced08a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668726"
---
# <a name="devenv-command-line-switches"></a>Devenv 命令行开关
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Devenv 可用来设置集成开发环境 (IDE) 的各个选项，以及从命令行生成、调试和部署项目。 使用这些开关从脚本或 .bat 文件（例如每夜生成的脚本）运行 IDE，或以特定配置启动 IDE。

> [!NOTE]
> 对于与生成相关的任务，现在推荐使用 MSBuild，而非 devenv。 有关详细信息，请参阅[命令行参考](../../msbuild/msbuild-command-line-reference.md)。

> [!NOTE]
> 必须以管理员身份运行 devenv 才能使用 [/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md) 和 [/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md) 开关。

## <a name="devenv-switch-syntax"></a>Devenv 开关语法
 默认情况下，devenv 命令将开关传递给 devenv.com 实用工具。

 devenv.com 实用工具用于通过标准系统流（如 `stdout` 和 `stderr`）传递输出，并在捕获输出时确定相应的 I/O 重定向（例如重定向到 .txt 文件）。 而以 `devenv.exe` 开头的命令可使用相同的开关，但会跳过 devenv.com 实用工具将其发送给 devenv.exe 程序。

 `devenv` 开关的语法规则与其他 DOS 命令行实用工具类似。 下列语法规则适用于所有 `devenv` 开关及其参数：

- 命令以 `devenv` 开头。

- 开关不区分大小写。

- 指定一个解决方案或项目时，第一个参数是解决方案文件或项目文件的名称，包括文件路径。

- 如果第一个参数是一个非解决方案或项目的文件，则该文件将在适当的编辑器中的 IDE 新实例中打开。

- 如果提供项目文件名而不是解决方案文件名，`devenv` 命令会在项目文件的父文件夹中搜索具有相同名称的解决方案文件。 例如，`devenv /build myproject1.vbproj` 命令会在父文件夹中搜索命名为“myproject1.sln”的解决方案文件。

    > [!NOTE]
    > 引用此项目的唯一一个解决方案文件应位于其父文件夹中。 如果父文件夹不包含引用此项目的解决方案文件，或父文件夹包含引用此项目的两个或更多解决方案文件，则将创建一个为此项目命名并引用此项目的临时解决方案文件。

- 当文件路径和文件名中包含空格时，必须用双引号 ("") 将它们括起来。 例如 "c:\project a\\"。

- 在同一行上的开关和参数之间插入一个空白字符。 例如，**devenv /log output.txt** 命令将打开 IDE，并将该会话的所有日志信息输出到 output.txt。

- 您无法在 `devenv` 命令中使用模式匹配语法。

## <a name="devenv-switches"></a>Devenv 开关
 使用下列命令行开关显示 IDE 并执行描述的任务。

|命令行开关|说明|
|-------------------------|-----------------|
|[/Command (devenv.exe)](../../ide/reference/command-devenv-exe.md)|启动 IDE 并执行指定的命令。|
|[/DebugExe (devenv.exe)](../../ide/reference/debugexe-devenv-exe.md)|在调试器的控制下加载 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 可执行文件。 此开关对 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 可执行文件不可用。 有关详细信息，请参阅[自动启动调试器中的进程](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger)。|
|[/LCID (devenv.exe)](../../ide/reference/lcid-devenv-exe.md) 或 `/l`|为 IDE 设置默认语言。 如果在 Visual Studio 的安装中不包括指定的语言，则将忽略此设置。|
|[/Log (devenv.exe)](../../ide/reference/log-devenv-exe.md)|启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 并将所有活动记录到日志文件中。|
|[/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md) 或 `/r`|编译并运行指定的解决方案。|
|[/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)|编译并运行指定的解决方案，在运行该解决方案时最小化 IDE，并在解决方案完成运行后关闭 IDE。|
|[/UseEnv (devenv.exe)](../../ide/reference/useenv-devenv-exe.md)|使 IDE 使用 PATH、INCLUDE 和 LIB 环境变量进行 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 编译，而不是使用“选项”  对话框中“项目”  选项的“VC++ 目录”节中指定的设置。 有关详细信息，请参阅[为命令行生成设置路径和环境变量](https://msdn.microsoft.com/library/99389528-deb5-43b9-b99a-03c8773ebaf4)|
|[/Edit (devenv.exe)](../../ide/reference/edit-devenv-exe.md)|在此应用程序的运行实例中打开指定的文件。 如果没有正在运行的实例，它将启动具有简化的窗口布局的新实例。|
|[/ResetAddin (devenv.exe)](../../ide/reference/resetaddin-devenv-exe.md)|启动 Visual Studio IDE 的实例而不加载指定的外接程序。|
|[/SafeMode (devenv.exe)](../../ide/reference/safemode-devenv-exe.md)|以安全模式启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，并仅加载默认的环境和服务以及第三方包的发布版。|
|[/ResetSkipPkgs (devenv.exe)](../../ide/reference/resetskippkgs-devenv-exe.md)|清除用户因希望避免加载有问题的 VSPackage 而添加到 VSPackage 中的所有 SkipLoading 标记。|
|[/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md)|强制 Visual Studio 合并所有可用的 VSPackage 中描述菜单、工具栏和命令组的资源元数据。|

 使用下列命令行开关执行描述的任务。 这些命令行开关不显示 IDE。

|命令行开关|说明|
|-------------------------|-----------------|
|[/? (devenv.exe)](../../ide/reference/q-devenv-exe.md)|在“命令提示符”  窗口中显示 devenv 开关的相关帮助信息。<br /><br /> **Devenv /?**|
|[/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)|根据指定解决方案的配置，生成指定的解决方案或项目。<br /><br /> **Devenv myproj.csproj /build**|
|[/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)|删除由生成命令创建的任何文件，而不影响源文件。<br /><br /> **Devenv myproj.csproj /clean**|
|[/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)|根据解决方案配置生成解决方案以及部署所需的文件。<br /><br /> **Devenv myproj.csproj /deploy**|
|[/Diff](../../ide/reference/diff.md)|比较两个文件。  采用四个参数：SourceFile、TargetFile、SourceDisplayName(optional)、TargetDisplayName(optional)。|
|[/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md)|注册位于 *\<VisualStudioInstallDir>* \Common7\IDE\ProjectTemplates 或 *\<VisualStudioInstallDir>* \Common7\IDE\ItemTemplates 的项目或项模板，以便能够通过“新建项目”  和“添加新项”  对话框访问它们。<br /><br /> **Devenv /InstallVSTemplates**|
|[/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)|用于在生成时指定一个文件来接收错误。<br /><br /> **Devenv myproj.csproj /build /out log.txt**|
|[/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)|要生成、清理或部署的项目。 仅当已提供 /build、/rebuild、/clean 或 /deploy 开关之后，才可使用此开关。|
|[/ProjectConfig (devenv.exe)](../../ide/reference/projectconfig-devenv-exe.md)|指定要生成或部署的项目配置。 仅当已提供 /project 开关之后，才可使用此开关。|
|[/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)|根据指定解决方案的配置，清理并生成指定的解决方案或项目。|
|[/ResetSettings (devenv.exe)](../../ide/reference/resetsettings-devenv-exe.md)|还原 Visual Studio 默认设置。 可以选择将这些设置重置为指定的 .vssettings 文件。|
|[/Updateconfiguration (devenv.exe)](../../ide/reference/updateconfiguration-devenv-exe.md)|通知 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 合并系统上的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 包，并检查 MEF 缓存中是否有任何更改。|
|[/Upgrade (devenv.exe)](../../ide/reference/upgrade-devenv-exe.md)|将指定的解决方案文件及其所有项目文件或指定的项目文件升级为这些文件的当前 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 格式。|

## <a name="see-also"></a>另请参阅
 [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
