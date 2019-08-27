---
title: 必须在安装后运行的命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d8a59e1a6613936c586c5529dcfc6a56a957112c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341994"
---
# <a name="commands-that-must-be-run-after-installation"></a>必须在安装后运行的命令
如果您将通过你扩展部署 *.msi*文件中，您必须运行**devenv /setup**作为您的安装顺序 for Visual Studio 以发现你的扩展的一部分。

> [!NOTE]
> 本主题中的信息适用于查找*devenv.exe*使用 Visual Studio 2008 及更早版本。 有关如何发现*devenv.exe*更高版本的 Visual Studio，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

## <a name="find-devenvexe"></a>查找 devenv.exe
 您可以找到每个版本*devenv.exe*从注册表值[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]编写安装程序，使用 RegLocator 表和 AppSearch 表作为属性存储的注册表值。 有关详细信息，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>RegLocator 表行，以查找来自不同版本的 Visual Studio 的 devenv.exe

|签名|根|键|名称|类型|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>AppSearch 相应 RegLocator 表行的表行

|属性|签名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 例如，在 Visual Studio 安装程序写入的注册表值**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath**作为*C:\VS2008\Common7\IDE\devenv.exe*，必须运行安装程序的可执行文件的完整路径。

> [!NOTE]
> RegLocator 类型表列为 2，因为它不需要签名表中指定其他版本信息。

## <a name="run-devenvexe"></a>运行 devenv.exe
 之后在安装程序中运行的标准操作 AppSearch，AppSearch 表中的每个属性具有值指向*devenv.exe*相应版本的 Visual Studio 的文件。 任何指定的注册表值是否不存在，因为未安装该版本的 Visual Studio-指定的属性设置为 null。

 Windows 安装程序支持通过自定义操作运行可执行文件属性指向键入 50。 自定义操作应包含在脚本执行选项中， `msidbCustomActionTypeInScript` (1024) 和`msidbCustomActionTypeCommit`(512)，以确保已成功将其集成到之前安装 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 有关详细信息，请参阅[CustomAction 表](https://docs.microsoft.com/windows/desktop/msi/customaction-table)并[自定义操作脚本中执行选项](https://docs.microsoft.com/windows/desktop/msi/custom-action-in-script-execution-options)。

 自定义操作类型 50 的指定属性作为源列和目标列中的命令行参数的值包含可执行文件。

### <a name="customaction-table-rows-to-run-devenvexe"></a>若要运行 devenv.exe 的 CustomAction 表行

|操作|类型|Source|Target|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 到 InstallExecuteSequence 表进行的安装过程的执行计划，必须编写自定义操作。 使用条件列的每一行中的相应属性以防止从正在运行，如果自定义操作的版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]系统上未安装。

> [!NOTE]
> Null 值的属性的计算结果为`False`在条件中使用时。

 每个自定义操作序列列的值取决于你的 Windows 安装程序包中的其他序列值。 序列值应该是这样*devenv.exe*自定义操作以运行尽可能接近之前 InstallFinalize 标准操作。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>InstallExecuteSequence 表来计划 devenv.exe 自定义操作

|操作|条件|序列|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>请参阅
- [使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)