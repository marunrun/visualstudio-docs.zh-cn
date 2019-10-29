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
ms.openlocfilehash: 7e85a03c71064687fdfbacf24b7aa59cd2a47f1a
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72982021"
---
# <a name="commands-that-must-be-run-after-installation"></a>必须在安装后运行的命令
如果通过 *.msi*文件部署扩展，则必须在安装过程中运行**Devenv/Setup** ，Visual Studio 才能发现扩展。

> [!NOTE]
> 本主题中的信息适用于通过 Visual Studio 2008 和更早版本查找*devenv。* 有关如何发现具有更高版本的 Visual Studio 的*devenv* ，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

## <a name="find-devenvexe"></a>查找 devenv
 你可以使用 RegLocator 表和 AppSearch 表将注册表值存储为属性，从注册表 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 值中查找每个版本的 node.js *。* 有关详细信息，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>RegLocator 表行，用于从不同版本的 Visual Studio 中查找 devenv

|签名|Root|项|“属性”|键入|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>对应 RegLocator 表行的 AppSearch 表行

|Property|签名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 例如，Visual Studio 安装程序将**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath**的注册表值作为*C:\VS2008\Common7\IDE\devenv.exe*写入到可执行文件的完整路径必须运行安装程序。

> [!NOTE]
> 因为 RegLocator 表的类型列是2，所以不需要在签名表中指定其他版本信息。

## <a name="run-devenvexe"></a>运行 devenv
 在安装程序中运行 AppSearch 标准操作后，AppSearch 表中的每个属性都有一个值，该值指向对应的 Visual Studio 版本的*devenv*文件。 如果不存在任何指定的注册表值（因为未安装该版本的 Visual Studio），则指定的属性将设置为 null。

 Windows Installer 支持运行属性指向自定义操作类型50的可执行文件。 自定义操作应包括脚本内执行选项（`msidbCustomActionTypeInScript` （1024）和 `msidbCustomActionTypeCommit` （512）），以确保 VSPackage 在集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]之前已成功安装。 有关详细信息，请参阅[CustomAction 表](/windows/desktop/msi/customaction-table)和[自定义操作的脚本执行选项](/windows/desktop/msi/custom-action-in-script-execution-options)。

 类型为50的自定义操作指定包含可执行文件的属性，作为目标列中源列和命令行参数的值。

### <a name="customaction-table-rows-to-run-devenvexe"></a>CustomAction 表行以运行 devenv

|操作|键入|源|Target|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 必须将自定义操作编写到 InstallExecuteSequence 表中，以便在安装过程中计划执行这些操作。 如果系统上未安装该版本的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，则使用 "条件" 列的每一行中的相应属性来防止自定义操作运行。

> [!NOTE]
> 如果在条件中使用，则 Null 值属性的计算结果为 `False`。

 每个自定义操作的序列列的值取决于 Windows Installer 包中的其他序列值。 序列值应为， *devenv*自定义操作在 InstallFinalize 标准操作之前尽可能接近。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>用于计划 devenv 自定义操作的 InstallExecuteSequence 表

|操作|条件|序列|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>请参阅
- [安装 Vspackage 与 Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)