---
title: “导入和导出设置”命令
ms.date: 11/21/2018
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 409c0f40adfd374065dedb842965d2d1237bc9a0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75568823"
---
# <a name="import-and-export-settings-command"></a>“导入和导出设置”命令

导入、导出或重置 Visual Studio 设置。

## <a name="syntax"></a>语法

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>开关

/export:`filename`

可选。 将当前设置导出到指定文件。

/import:`filename`

可选。 导入指定文件中的设置。

/reset

可选。 重置当前设置。

## <a name="remarks"></a>备注

不带任何开关运行此命令将打开“导入和导出设置”向导  。 有关详细信息，请参阅[同步设置](../synchronized-settings-in-visual-studio.md)和[环境设置](../environment-settings.md)。

## <a name="example"></a>示例

以下命令将当前设置导出到文件 `MyFile.vssettings`：

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```

## <a name="see-also"></a>请参阅

- [环境设置](../../ide/environment-settings.md)
- [同步设置](../../ide/synchronized-settings-in-visual-studio.md)
- [个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
