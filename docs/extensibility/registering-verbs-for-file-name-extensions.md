---
title: 注册文件名扩展名的谓词 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ac2854f1799075cc14d9beb557335be5228be21d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701537"
---
# <a name="register-verbs-for-file-name-extensions"></a>注册文件名扩展名的谓词
文件名扩展名与应用程序的关联通常具有用户双击文件时发生的首选操作。 此首选操作链接到与操作对应的谓词（例如打开）。

 可以使用位于**HKEY_CLASSES_ROOT\{progid_shell**的 Shell 键注册与编程标识符 （ProgID） 关联的谓词。 有关详细信息，请参阅[文件类型](/windows/desktop/shell/fa-file-types)。

## <a name="register-standard-verbs"></a>注册标准动词
 操作系统识别以下标准动词：

- 打开

- 编辑

- 显示

- Print

- 预览

  只要有可能，注册一个标准动词。 最常见的选择是"打开"谓词。 仅当打开文件和编辑文件之间存在明显区别时，才使用 Edit 谓词。 例如，打开 *.htm*文件会在浏览器中显示它，而编辑 *.htm*文件将启动 HTML 编辑器。 标准谓词随操作系统区域设置进行本地化。

> [!NOTE]
> 注册标准谓词时，不要为 Open 键设置默认值。 默认值包含菜单上的显示字符串。 操作系统为标准动词提供此字符串。

 应注册项目文件以启动用户打开文件[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]时的新实例。 下面的示例说明了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]项目的标准谓词注册。

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

 要在 的现有实例中打开文件[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，请注册 DDEEXEC 密钥。 下面的示例演示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]*.cs*文件的标准谓词注册。

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

## <a name="set-the-default-verb"></a>设置默认动词
 默认谓词是当用户双击 Windows 资源管理器中的文件时执行的操作。 默认谓词是指定为**HKEY_CLASSES_ROOT\\*progid*_Shell**键的默认值的谓词。 如果未指定值，则默认谓词是**HKEY_CLASSES_ROOT\\*progid*_Shell**键列表中指定的第一个谓词。

> [!NOTE]
> 如果计划更改并行部署中扩展的默认谓词，请考虑对安装和删除的影响。 在安装过程中，将覆盖原始默认值。

## <a name="see-also"></a>请参阅
- [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md)
