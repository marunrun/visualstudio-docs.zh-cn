---
title: 注册文件扩展名的谓词 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af86781f771ec5516e212ba3df8fdf945cd8d6d3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334223"
---
# <a name="register-verbs-for-file-name-extensions"></a>注册文件扩展名的谓词
与应用程序的文件扩展名关联通常具有首选的操作，当用户双击文件时发生。 此首选的操作链接到动词，例如打开对应于该操作。

 您可以注册使用 Shell 密钥扩展位于与编程标识符 (ProgID) 关联的谓词**HKEY_CLASSES_ROOT\{progid} \shell**。 有关详细信息，请参阅[文件类型](/windows/desktop/shell/fa-file-types)。

## <a name="register-standard-verbs"></a>注册标准谓词
 操作系统识别出以下标准谓词：

- 打开

- Edit

- 播放

- 的

- 预览

  只要有可能，注册标准谓词。 最常见的选择是动词 Open。 仅当没有打开的文件和编辑文件之间有明显差异，请使用编辑谓词。 例如，打开 *.htm*文件将其显示在浏览器中，而编辑 *.htm*文件启动 HTML 编辑器。 标准谓词已本地化的操作系统的区域设置。

> [!NOTE]
> 注册标准谓词时, 未设置的默认值为打开的注册表。 默认值包含在菜单上的显示字符串。 操作系统提供标准谓词此字符串。

 项目文件应注册为在启动的新实例[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]当用户在打开该文件。 下面的示例演示了标准谓词注册[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]项目。

```
[HKEY_CLASSES_ROOT\.csproj]
@="VisualStudio.csproj.8.0"

[HKEY_CLASSES_ROOT\.csproj\OpenWithList]
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]
@=""

[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]
"VisualStudio.csproj.8.0"=""

[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]
@="C# Project file"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""
```

 若要打开一个文件中的现有实例[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，注册 DDEEXEC 密钥。 下面的示例演示的标准谓词登记[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] *.cs*文件。

```
[HKEY_CLASSES_ROOT\.cs]
@="VisualStudio.cs.8.0"

[HKEY_CLASSES_ROOT\.cs\OpenWithList]
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]
@=""

[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]
"VisualStudio.cs.8.0"=""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]
@="C# Source file"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]
@="Open(\"%1\")"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]
@="VisualStudio.8.0"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]
@="system"
```

## <a name="set-the-default-verb"></a>设置默认的谓词
 默认的谓词是当用户双击 Windows 资源管理器中的文件执行的操作。 默认的谓词是指定的默认值为动词**HKEY_CLASSES_ROOT\\*progid*\Shell**密钥。 如果未不指定任何值，默认谓词是中指定的第一个动作**HKEY_CLASSES_ROOT\\*progid*\Shell**键列表。

> [!NOTE]
> 如果你打算更改默认的谓词中的并行部署的扩展插件，请考虑对安装和删除的影响。 在安装过程中会覆盖原始默认值。

## <a name="see-also"></a>请参阅
- [管理通过并行文件关联](../extensibility/managing-side-by-side-file-associations.md)
