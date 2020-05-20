---
title: “选项”对话框 ->“环境”->“自动恢复”
ms.date: 11/04/2016
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
ms.openlocfilehash: 81493379cf847251124d2ab4fd0a978abd96af8f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585660"
---
# <a name="autorecover-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“自动恢复”

使用“选项”对话框中的此页面可指定是否自动备份文件  。 如果 Visual Studio 意外关闭，还可以指定是否要还原已修改的文件。

选择“工具”菜单，然后选择“选项”，再选择“环境” > “自动恢复”，即可访问此对话框。 如果此页未出现在列表中，请在“选项”对话框中选择“显示所有设置”   。

**每隔 [n] 分钟保存一次自动恢复信息**

使用此选项可以自定义在编辑器中自动保存文件的频率。 对于以前保存的文件，该文件的副本保存在 %USERPROFILE%\Documents\Visual Studio\\[version]\Backup Files\\[projectname] 中。 如果文件是新文件但尚未保存，则将使用一个随机生成的文件名自动保存。

**保留自动恢复信息 [n] 天**

使用此选项可指定 Visual Studio 将为自动恢复创建的文件保留多长时间。

### <a name="see-also"></a>另请参阅

- [“选项”对话框](../../ide/reference/options-dialog-box-visual-studio.md)
