---
title: 同步设置
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.RoamingSettings
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6459b6f65fd1e29fbadb01f6aa2fc51520b726b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646818"
---
# <a name="synchronized-settings-in-visual-studio"></a>Visual Studio 中的同步设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用同一个性化帐户在多台计算机上登录 Visual Studio 时，默认情况下你的设置会在所有计算机上进行同步。

## <a name="synchronized-settings"></a>同步设置
 默认情况下，以下设置会进行同步。

- 开发设置（必须在首次运行 Visual Studio 时选择一组设置，但是可以随时更改选择。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

- “工具”|“选项”**** 页中的以下选项：

  - “主题”**** 和菜单栏大小写设置（位于“环境”****、“常规”**** 选项页上）

  - “环境”****、“字体和颜色”**** 选项页上的所有设置

  - 所有键盘快捷方式（位于“环境”****、“键盘”**** 选项页上）

  - “环境、选项卡和窗口”**** 选项页上的所有设置

  - “环境”****、“启动”**** 选项页上的所有设置

  - " **文本编辑器** " 选项页上的所有设置

- “XAML 设计器”选项页上的所有设置

- 用户定义的命令别名。 有关如何定义命令别名的详细信息，请参阅 [Visual Studio 命令别名](../ide/reference/visual-studio-command-aliases.md)。

- “窗口”|“管理窗口布局”**** 页中用户定义的窗口布局

## <a name="turning-synchronized-settings-off-for-a-particular-computer"></a>关闭特定计算机的同步设置
 默认情况下启用 Visual Studio 的同步设置。 可以通过转到“工具”|“选项”|“环境”|“同步设置”**** 页并取消选中复选框，来关闭计算机上的同步设置。  例如，如果你决定不同步计算机 A 上的 Visual Studio 设置，那么计算机 A 上的任何设置更改将不会出现在计算机 B 或计算机 C 上。计算机 B 和 C 将继续彼此同步，但不与计算机 A 同步。

## <a name="synchronizing-settings-across-visual-studio-family-products-and-editions"></a>在 Visual Studio 系列产品和版本之间同步设置
 可以在 Visual Studio 2015 的任何版本（包括 Express 和 Community）之间同步设置。 Visual Studio 系列产品（如 Blend）之间的设置也是同步的。 但是，这些系列产品中的每一个都可能具有它自己与 Visual Studio 不共享的设置。 例如，特定于计算机 A 上的 Blend 设置将与计算机 B 上的 Blend 共享，但不与计算机 A 或 B 上的 Visual Studio 共享。

> [!WARNING]
> Visual Studio 2013 和 Visual Studio 2015 之间不同步设置。 首次打开 Visual Studio 2015 时，将迁移 Visual Studio 2013 的设置，但此后无法将其迁移回 Visual Studio 2013。

## <a name="see-also"></a>另请参阅
 [个性化设置 IDE](../ide/personalizing-the-visual-studio-ide.md)
