---
title: 自定义 IDE
ms.date: 11/20/2017
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2961730594abd268ae130cf2c3d2b93df5322c14
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68606078"
---
# <a name="personalize-the-visual-studio-ide"></a>个性化设置 Visual Studio IDE

可以通过各种方法对 Visual Studio 进行个性化设置，来为自己的开发风格和需求提供最佳支持。 许多设置跨 Visual Studio 实例出现（请参阅[同步设置](../ide/synchronized-settings-in-visual-studio.md)）。 本文简要介绍不同的个性化设置以及可以获取详细信息的位置。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[自定义 Visual Studio for Mac IDE](/visualstudio/mac/customizing-the-ide)。

## <a name="default-settings"></a>默认设置

可选择一组默认设置，以便根据开发类型优化 Visual Studio。 有关详细信息，请参阅[环境设置](environment-settings.md)。

## <a name="general-environment-options"></a>常规环境选项

许多个性化设置选项会通过“[环境选项](../ide/reference/general-environment-options-dialog-box.md)”对话框公开。 可通过两种方法来访问此对话框：

- 在菜单栏上，依次选择“工具” > “选项”，如果尚未展开，则请展开“环境”节点。   

- 按 Ctrl+Q，在搜索框中键入“环境”，然后从结果中选择“环境”>“常规”     。

> [!TIP]
> 出现“选项”对话框后，可按 F1  获取有关该页面上的各种设置的帮助。

## <a name="environment-color-themes"></a>环境颜色主题

要在浅色、深色和蓝色之间更改颜色主题，请在搜索框中键入“环境”，然后选择“环境”>“常规”   。 在“选项”对话框中，更改“颜色主题”选项。  

要更改编辑器中的着色选项，请在搜索框中键入“环境”，然后选择“环境”>“字体和颜色”   。 请参阅[如何：更改字体和颜色](../ide/how-to-change-fonts-and-colors-in-visual-studio.md)。

### <a name="main-menu-casing"></a>主菜单中的大小写

可以在“词首字母大写”（如“File”）和“全部大写”（如“FILE”）之间更改主菜单大小写。   在搜索框中键入“环境”，选择“环境”>“常规”，然后更改“将词首字母大写样式应用到菜单栏”选项    。

### <a name="customize-menus-and-toolbars"></a>自定义菜单和工具栏

若要添加或删除菜单或者工具栏项，请参阅[如何：自定义菜单和工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)。

::: moniker range="vs-2017"

## <a name="start-page"></a>起始页

若要为你和你的团队创建自定义起始页，请参阅[自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。

::: moniker-end

## <a name="window-layouts"></a>窗口布局

你可以定义和保存多个窗口布局并在它们之间切换。 例如，可以定义一个用于编码的布局和一个用于调试的布局。 若要安排窗口的位置和行为，并保存自定义布局，请参阅[自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。

## <a name="external-tools"></a>外部工具

可以自定义“工具”菜单以启动外部工具  。 有关详细信息，请参阅[管理外部工具](../ide/managing-external-tools.md)。

## <a name="see-also"></a>请参阅

- [环境设置](environment-settings.md)
- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
- [快速入门：初步了解 Visual Studio IDE](../ide/quickstart-ide-orientation.md)
- [自定义 Visual Studio for Mac IDE](/visualstudio/mac/customizing-the-ide)