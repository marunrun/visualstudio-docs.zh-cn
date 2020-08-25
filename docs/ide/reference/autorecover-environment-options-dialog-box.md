---
title: “选项”对话框 ->“环境”->“自动恢复”
ms.date: 08/14/2020
ms.topic: reference
f1_keywords:
- VS.DialogAutoRestore
- VS.ToolsOptionsPages.Environment.AutoRecover
- VS.ToolsOptionsPages.Environment.Auto_Save_and_Restore
helpviewer_keywords:
- files, recovering
- AutoRecover page
- saving files, automatically
- files, saving automatically
ms.assetid: 397e5e44-4bbe-4289-94d1-642b466c9111
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f35424089b293b858c609d19f59459693373eb4d
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88250273"
---
# <a name="autorecover-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“自动恢复”

使用“选项”对话框中的此页面可指定是否自动备份文件  。 如果 Visual Studio 意外关闭，还可以指定是否要还原已修改的文件。

若要访问此对话框，请依次转到“工具” > “选项” > “环境” > “自动恢复”   。

:::image type="content" source="media/autorecover-options.png" alt-text="“选项”对话框中“自动恢复”部分的屏幕截图":::

**每隔 [n] 分钟保存一次自动恢复信息**

::: moniker range="vs-2019"

使用此选项可以自定义在编辑器中自动保存文件的频率。 对于以前保存的文件，Visual Studio 2019 版本 16.2 及更高版本会在 %LocalAppData%\Microsoft\VisualStudio\BackupFiles\\[projectname] 中保存文件副本。 如果文件是新文件但尚未保存，则 Visual Studio 会使用一个随机生成的文件名自动保存它。

> [!NOTE]
> 如果使用的是 Visual Studio 2019 版本 16.1 或更早版本，则文件位于 %USERPROFILE%\Documents\Visual Studio [version]\Backup Files\\[projectname]。 有关详细信息，请参阅 [Visual Studio 2019 发行说明历史记录](/visualstudio/releases/2019/release-notes-history/)页面。

::: moniker-end

::: moniker range="vs-2017"

使用此选项可以自定义在编辑器中自动保存文件的频率。 对于以前保存的文件，Visual Studio 2017 会在 %USERPROFILE%\Documents\Visual Studio [version]\Backup Files\\[projectname] 中保存文件副本。 如果文件是新文件但尚未保存，则 Visual Studio 会使用一个随机生成的文件名自动保存它。

::: moniker-end

**保留自动恢复信息 [n] 天**

使用此选项可指定 Visual Studio 将为自动恢复创建的文件保留多长时间。

### <a name="see-also"></a>另请参阅

- [“选项”对话框](../../ide/reference/options-dialog-box-visual-studio.md)
