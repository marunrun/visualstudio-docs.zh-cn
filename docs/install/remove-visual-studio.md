---
title: 删除 Visual Studio
titleSuffix: ''
description: 了解如何逐步从计算机中彻底删除 Visual Studio。
ms.date: 12/19/2019
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- uninstall
- uninstall Visual Studio
- remove
- remove Visual Studio
- cleanup
- cleanup Visual Studio
- clean up
- clean up Visual Studio
ms.assetid: 9c81a777-9c95-4934-b517-c60c6dc78799
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: b0e8c8fe10451e9e5906eabf7f4f65086d147904
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76113709"
---
# <a name="remove-visual-studio"></a>删除 Visual Studio

如果遇到灾难性错误，并且无法修复或卸载 Visual Studio，可运行 `InstallCleanup.exe` 工具，以删除 Visual Studio 2017 或 Visual Studio 2019 的所有已安装实例的安装文件和产品信息。

> [!WARNING]
> InstallCleanup 工具仅作为修复或卸载失败时在不得已情况下采用的一种方法  。 此工具可能会从其他 Visual Studio 安装或其他产品中卸载功能，可能还需要修复或重新安装这些功能。

## <a name="run-installcleanupexe"></a>运行 InstallCleanup.exe

可以将以下任一命令行开关与 `InstallCleanup.exe` 工具结合使用：

| 开关 | 行为 |
| ------ | -------- |
| `-i`   | 如果没有传递其他开关，则此开关为默认值。 它仅删除主安装目录和产品信息。 如果打算在运行 `InstallCleanup.exe` 工具后重新安装相同版本的 Visual Studio，则使用此开关。 |
| `-f`   | 此开关删除在安装目录外安装的主安装目录、产品信息和大部分其他功能，这些功能也可能与其他 Visual Studio 安装或其他产品共享。 如果打算删除 Visual Studio 并且后来不重新安装，则使用此开关。 |

以下是运行 `InstallCleanup.exe` 工具的方法：

1. 关闭 Visual Studio 安装程序。
1. 打开管理员命令提示符。 要打开管理员命令提示符，请执行以下步骤：
   * 在“在此键入进行搜索”框中键入“cmd”  。
   * 右键单击“命令提示符”  ，然后选择“以管理员身份运行”  。
1. 输入 `InstallCleanup.exe` 工具的完整路径，并添加所需的命令行开关。 默认情况下，此工具的路径如下所示：

   ```
   C:\Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout\InstallCleanup.exe
   ```

   > [!NOTE]
   > 如果在 Visual Studio 安装程序目录下找不到 `InstallCleanup.exe`，而该目录始终位于 `%ProgramFiles(x86)%\Microsoft Visual Studio`，则接下来要执行以下操作。 按照指示来[安装 Visual Studio](install-visual-studio.md)。 然后，在显示工作负载选择屏幕时，关闭窗口并再次执行此页上的步骤。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [修改 Visual Studio](modify-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
