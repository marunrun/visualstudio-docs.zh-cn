---
title: 同步设置
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9f567e07ea085844672f04194e4a4ffc5a9318e4
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824811"
---
# <a name="synchronize-visual-studio-settings-across-multiple-computers"></a>跨多台计算机同步 Visual Studio 设置

使用同一个性化帐户在多台计算机上登录 Visual Studio 时，可跨计算机同步设置。

## <a name="synchronized-settings"></a>同步设置

默认情况下，以下设置会进行同步：

- 开发设置。 需要在首次打开 Visual Studio 时选择设置集合，但是可以随时更改选择。 有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

- 用户定义的命令别名。 有关如何定义命令别名的详细信息，请参阅 [Visual Studio 命令别名](../ide/reference/visual-studio-command-aliases.md)。

- “窗口” > “管理窗口布局”页中用户定义的窗口布局   。

- “工具”   > “选项”  页中的以下选项：

  - “主题”和菜单栏大小写设置（位于“环境” > “常规”选项页上）   。

  - “环境” > “字体和颜色”选项页上的所有设置   。

  - 所有键盘快捷方式（位于“环境” > “键盘”选项页上）   。

  - “环境” > “选项卡和窗口”选项页上的所有设置   。

  - “环境” > “启动”选项页上的所有设置   。

  -  “文本编辑器”选项页上的所有设置，例如，[代码样式首选项](code-styles-and-code-cleanup.md)。

  - “XAML 设计器”选项页上的所有设置  。

## <a name="turn-off-synchronized-settings-on-a-particular-computer"></a>关闭特定计算机上的同步设置

默认情况下启用 Visual Studio 的同步设置。 可以通过转到“工具” > “选项” > “环境” > “帐户”页并取消选中“登录到 Visual Studio 时，跨设备同步设置”，关闭计算机上的同步设置      。

例如，如果决定不同步计算机“A”上的 Visual Studio 设置，那么计算机“A”上的任何设置更改将不会出现在计算机“B”或计算机“C”上。 计算机“B”和“C”将继续与彼此同步，但不与计算机“A”同步。

> [!NOTE]
> 如果通过取消选择“工具” > “选项” > “环境” > 帐户页面上的选项选择不对设置进行同步，那么同一台计算机上其他版本的 Visual Studio 不会受到影响     。 那些 Visual Studio 的并行安装将继续同步其设置（除非取消选中该选项）。

## <a name="synchronize-settings-across-visual-studio-family-products-and-editions"></a>在 Visual Studio 系列产品和版本之间同步设置

并行安装的各版本的 Visual Studio 设置之间进行了同步  。 Visual Studio 系列产品（包括 Blend for Visual Studio）之间的设置也是同步的。 但是，系列产品中的每一个都可能具有它自己的、与 Visual Studio 不共享的设置。 例如，特定于计算机 A 上 Blend for Visual Studio 的设置不与计算机 A 或 B 上的 Visual Studio 共享。

## <a name="side-by-side-synchronized-settings"></a>并排同步设置

::: moniker range="vs-2017"

某些设置（如工具窗口布局）不会在 Visual Studio 的不同并行安装之间共享。 %userprofile%\Documents\Visual Studio 2017\Settings 中的 CurrentSettings.vssettings 文件位于特定于安装的文件夹中，该文件夹类似于 %localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx\Settings    。

> [!NOTE]
> 要使用新的特定于安装的设置，请进行全新安装。 升级现有 Visual Studio 安装时，它将使用现有共享位置。

如果现在已拥有 Visual Studio 的并行安装，并希望使用特定于安装的新设置文件位置，请执行以下步骤：

1. 升级到 Visual Studio 2017 版本 15.3 或更高版本。

2. 使用“导入\导出”设置向导将所有现有设置导出到“%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx”文件夹之外的某个位置   。

3. 打开“VS 2017 开发人员命令提示”并运行 `devenv /resetuserdata`  。

1. 打开 Visual Studio，并从导出的设置文件中导入已保存的设置。

::: moniker-end

::: moniker range=">=vs-2019"

某些设置（如工具窗口布局）不会在 Visual Studio 的不同并行安装之间共享。 %userprofile%\Documents\Visual Studio 2019\Settings 中的 CurrentSettings.vssettings 文件位于特定于安装的文件夹中，该文件夹类似于 %localappdata%\Microsoft\VisualStudio\16.0_xxxxxxxx\Settings    。

::: moniker-end

## <a name="see-also"></a>请参阅

- [个性化 IDE](../ide/personalizing-the-visual-studio-ide.md)
- [环境设置](../ide/environment-settings.md)
- [“环境”>“帐户选项”对话框](reference/accounts-environment-options-dialog-box.md)
