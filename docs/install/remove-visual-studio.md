---
title: 删除 Visual Studio
titleSuffix: ''
description: 了解如何逐步从计算机中彻底删除 Visual Studio。
ms.date: 03/30/2019
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
author: heaths
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e363065d96169660817a548fb97d39f09cf679c9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810385"
---
# <a name="remove-visual-studio"></a>删除 Visual Studio

如果遇到灾难性错误，并且无法修复或卸载 Visual Studio，可运行 `InstallCleanup.exe` 工具，以删除 Visual Studio 2017 或 Visual Studio 2019 的所有已安装实例的安装文件和产品信息。 如果修复或卸载失败，运行此工具应仅作为最后的解决措施，并且可能从其他 Visual Studio 安装或其他也可能需要修复的产品中卸载功能。

在以下说明中，可以使用具有以下行为的不同命令行开关运行此工具：

| 开关 | 行为 |
| ------ | -------- |
| `-i`   | 如果没有传递其他开关，则默认为此开关，并且仅删除主安装目录和产品信息。 如果打算在运行 `InstallCleanup.exe` 工具后重新安装相同的版本，则首选此行为。 |
| `-f`   | 如果指定此开关，则会删除在安装目录外安装的主安装目录、产品信息和大部分其他功能，这些功能可能与其他 Visual Studio 安装或其他产品共享。 如果打算删除 Visual Studio 并且后来不重新安装，则首选此行为。 |

1. 关闭 Visual Studio 安装程序。
2. 打开管理员命令提示符。 要打开管理员命令提示符，请执行以下步骤：
   * 在“在此键入进行搜索”框中键入“cmd”。
   * 右键单击“命令提示符” ，然后单击“以管理员身份运行” 。
3. 键入 `InstallCleanup.exe` 实用工具的完整路径，并传递所需的任何命令行开关。 默认情况下，此实用工具的路径如下所示：

   ```
   C:\Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout\InstallCleanup.exe
   ```

如果在 Visual Studio 安装程序目录下（始终位于 `%ProgramFiles(x86)%\Microsoft Visual Studio`）没有找到 `InstallCleanup.exe`，请按照说明[安装 Visual Studio](install-visual-studio.md)，并在显示工作负载选择屏幕时关闭窗口，再按照前面的步骤执行。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [修改 Visual Studio](modify-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
