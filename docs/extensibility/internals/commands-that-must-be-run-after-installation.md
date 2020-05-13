---
title: 安装后必须运行的命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 77add5afd5d44358f0077a11bb70559a796e74c6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709475"
---
# <a name="commands-that-must-be-run-after-installation"></a>安装后必须运行的命令
如果通过 *.msi*文件部署扩展，则必须在安装时运行**devenv /setup，** 以便 Visual Studio 发现扩展。

> [!NOTE]
> 本主题中的信息适用于在 Visual Studio 2008 和更早版本查找*devenv.exe。* 有关如何使用 Visual Studio 的更高版本发现*devenv.exe*的信息，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

## <a name="find-devenvexe"></a>查找 devenv.exe
 您可以使用 RegLocator 表和 AppSearch 表从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]安装程序编写的注册表值中查找每个版本的*devenv.exe，* 将注册表值存储为属性。 有关详细信息，请参阅[检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>RegLocator 表行，用于查找不同版本的 Visual Studio 的 devenv.exe

|签名|Root|密钥|名称|类型|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|软件_微软_VisualStudio_7.0\设置_VS|环境路径|2|
|RL_DevenvExe_2003|2|软件_微软_视觉工作室\7.1\设置_VS|环境路径|2|
|RL_DevenvExe_2005|2|软件_微软_VisualStudio_8.0\设置_VS|环境路径|2|
|RL_DevenvExe_2008|2|软件_微软_VisualStudio_9.0\设置_VS|环境路径|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>相应 RegLocator 表行的应用搜索表行

|properties|签名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 例如，Visual Studio 安装程序将注册表值**HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_9.0_安装程序_VS_环境路径**写入*C：_VS2008_Common7_IDE_devenv.exe，* 安装程序必须运行的可执行文件的完整路径。

> [!NOTE]
> 由于 RegLocator 表的类型列为 2，因此无需在签名表中指定其他版本信息。

## <a name="run-devenvexe"></a>运行 devenv.exe
 在安装程序中运行 AppSearch 标准操作后，AppSearch 表中的每个属性都有一个值，指向相应版本的 Visual Studio 的*devenv.exe*文件。 如果不存在任何指定的注册表值（因为未安装该版本的 Visual Studio），则指定属性设置为 null。

 Windows 安装程序支持运行一个可执行文件，属性通过自定义操作类型 50 指向该可执行文件。 自定义操作应包括脚本内执行选项`msidbCustomActionTypeInScript`（1024） 和`msidbCustomActionTypeCommit`（512），以确保 VSPackage 已成功安装，然后再将其集成到 中。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 有关详细信息，请参阅[自定义操作表](/windows/desktop/msi/customaction-table)和[自定义操作在脚本内执行选项](/windows/desktop/msi/custom-action-in-script-execution-options)。

 类型 50 的自定义操作指定包含可执行文件的属性作为"目标"列中的 Source 列和命令行参数的值。

### <a name="customaction-table-rows-to-run-devenvexe"></a>要运行 devenv.exe 的自定义操作表行

|操作|类型|源|目标|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/设置|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/设置|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/设置|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/设置|

 必须将自定义操作创作到"安装执行顺序"表中，以安排它们在安装期间执行。 在"条件"列的每一行中使用相应的属性，以防止在系统上未安装该[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]版本的自定义操作。

> [!NOTE]
> 在条件中使用时，将`False`空值属性计算为

 每个自定义操作的序列列的值取决于 Windows 安装程序包中的其他序列值。 序列值应使*devenv.exe*自定义操作尽可能接近安装 Finalize 标准操作之前。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>安装执行序列表以安排 devenv.exe 自定义操作

|操作|条件|序列|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>请参阅
- [使用 Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
