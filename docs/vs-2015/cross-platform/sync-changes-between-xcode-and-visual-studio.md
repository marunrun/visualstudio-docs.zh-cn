---
title: 在 XCode 和 Visual Studio 2015 之间的更改同步 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c71a4d7c-120e-4559-a114-3a99c4b860a9
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 42352ba4c5260c4b13a4cb3c6875d3469efcf404
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62573368"
---
# <a name="sync-changes-between-xcode-and-visual-studio"></a>在 XCode 和 Visual Studio 之间同步更改
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于移动开发的 Microsoft Visual C++ 组件包括在电脑和 Mac 间同步工作的远程功能。 Visual Studio 和 Mac 计算机配对后，向 Visual Studio 中的 iOS 应用程序项目提供新选项，可用于在 XCode 中打开项目、在 XCode 和 Visual Studio 间移动代码，并可清理临时 XCode 项目目录。

 若要使用远程计算机选项，你的项目必须是 iOS 应用程序项目，且 Visual Studio 必须与你的 Mac 进行配对。 有关如何进行 Mac 配对的先决条件和说明，请参阅[安装和配置使用 iOS 进行构建的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。

## <a name="the-remote-machine-menu"></a>“远程计算机”菜单
 在“解决方案资源管理器”中，右键单击 iOS 应用程序项目以显示上下文菜单。 选择“远程计算机”项，显示可用的远程选项。

 ![解决方案资源管理器中的“远程计算机”菜单项](../cross-platform/media/cppmdd-u2-remotemachine-menu.jpg "CPPMDD_U2_RemoteMachine_Menu")

 通过这些命令，可在 XCode 中打开项目，在 Visual Studio 和 XCode 之间移动本地更改或整个项目，并可清理远程计算机上的临时文件。

### <a name="open-in-xcode"></a>在 XCode 中打开
 若要从 Visual Studio 打开 XCode 中的项目，请在“远程计算机”子菜单上选择“在 XCode 中打开”以便在配对的远程计算机上打开所选项目。 vcremote 服务器用于在 Mac 上打开 XCode，并导航到 Mac 上创建的包含项目副本的临时目录。 Visual Studio 会弹出一个对话框，显示用于项目的临时目录。 远程计算机上执行的操作也会在 Visual Studio 的“输出”窗口中显示。 若要查看它们，可能需要在“输出”窗口顶部的“显示输出”下拉菜单中选择“Visual C++ 远程计算机”。

 ![“输出”窗口显示远程计算机操作。](../cross-platform/media/cppmdd-u2-remotemachine-output.png "CPPMDD_U2_RemoteMachine_Output")

 在 Mac 上，可通过任意 XCode 工具编辑代码和资源、情节提要以及操作。 iOS 应用程序项目在 Visual Studio 中注释为“在 XCode 中打开”，这表示可能在远程计算机上进行了更改。 编辑完成后，可使用“从远程拉取”或“从远程增量拉取”命令将更改复制回 Visual Studio 项目。

### <a name="push-to-remote-and-incremental-push-to-remote"></a>推送到远程和增量推送到远程
 如果在 Visual Studio 中更改了 iOS 应用程序项目，则可使用“推送到远程”和“增量推送到远程”命令将更改后的项目文件移动到配对的远程计算机。 “推送到远程”命令将所有项目文件复制到远程计算机。 “增量推送到远程”命令仅将更改的文件复制到远程计算机。 对于更改较小的大型项目，增量命令可节省时间和带宽。

 若要将项目文件复制到 Mac，请在 Visual Studio 的“解决方案资源管理器”窗口中，右键单击 iOS 应用程序项目打开上下文菜单。 选择“远程计算机”，然后选择“推送到远程”或“增量推送到远程”，将项目文件从 Visual Studio 复制到 Mac。

### <a name="pull-from-remote-and-incremental-pull-from-remote"></a>从远程拉取和从远程增量拉取
 在 XCode 中更改项目后，将更改移回 Visual Studio 以保持项目同步。

 若要从 Mac 复制项目文件，请在 Visual Studio 的“解决方案资源管理器”窗口中，右键单击 iOS 应用程序项目打开上下文菜单。 选择“远程计算机”，然后选择“从远程拉取”或“从远程增量拉取”，将项目文件从 Mac 复制到 Visual Studio。

### <a name="clean-remote"></a>远程清理
 可使用“远程清理”命令删除远程计算机上临时项目目录中的文件。 将删除 Mac 上的目录内容（包括所有源文件或生成产品）。 使用“远程清理”命令之前，请确保已使用“从远程拉取”或“从远程增量拉取”同步了所有要返回到 Visual Studio 的更改。

 若要清理远程计算机上的临时项目目录，请在 Visual Studio 的“解决方案资源管理器”窗口中，右键单击 iOS 应用程序项目打开上下文菜单。 选择“远程计算机”，然后选择“远程清理”以删除 Mac 中的项目目录文件。
