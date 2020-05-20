---
title: 适用于 R 的包管理器
description: 如何在 Visual Studio 中使用 R 程序包管理器来安装和管理 R 程序包。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: d35bfd45e862912ff78ae600eed01ce8dc002493
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62998847"
---
# <a name="package-manager"></a>程序包管理器

针对 Visual Studio 的 R 工具 (RTVS) 程序包管理器是一个用于管理 R 程序包的UI。 若要打开它，请选择“R 工具” > “窗口” > “程序包”或按 Ctrl+7。

程序包管理器包含三个选项卡。 每个选项卡均在左侧显示相关程序包的列表，右侧显示所选程序包的特定详细信息，包括程序包版本、说明、许可证、安装位置和指向其他相关信息的链接。 右上角的搜索框可用于筛选列表。

> [!Tip]
> 在选项卡之间切换时，搜索框中的词语保持有效。

- “可用”  用于浏览要安装的程序包。 如果已安装程序包，右侧的“安装”按钮会改为“卸载”   。

    ![针对 Visual Studio 的 R 工具程序包管理器中的可用程序包选项卡](media/package-manager-available.png)

- “已安装”  显示所有已安装和已加载的程序包。 程序包旁边的绿色园点指示该程序包已加载到 R 会话中。 左侧的红色 X 图标或右侧的“卸载”  按钮可用于卸载程序包。 如果有较新版本的已安装程序包可用，可通过程序包右侧的蓝色向上箭头执行更新。

    ![针对 Visual Studio 的 R 工具程序包管理器中的已安装程序包选项卡](media/package-manager-installed.png)

- “已加载”仅显示已加载到 R 会话中的程序包，显示的所有程序包都会带有绿色圆点  。 还可在此处卸载和更新程序包。

    ![针对 Visual Studio 的 R 工具程序包管理器中的已加载程序包选项卡](media/package-manager-loaded.png)

## <a name="package-locations"></a>程序包位置

程序包安装在以下位置:

- RTVS 附带的核心程序包安装在 C:\Program Files\Microsoft\R Client\R_SERVER\library  中
- 其他程序包安装到了 %userprofile%\Documents\R\win-library\3.3 
