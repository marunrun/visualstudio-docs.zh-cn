---
title: 设置 Subversion 存储库
description: 使用 Visual Studio for Mac 中的 Subversion。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 0D58FB37-530E-495B-BED6-FD499477A9B6
ms.openlocfilehash: 7133ffd01d8f384efa91d95bc8ea05aa75b7dd0d
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74985226"
---
# <a name="set-up-a-subversion-repository"></a>设置 Subversion 存储库

Subversion 是一个集中式版本控制系统  ，这表示，存在一个服务器包含所有文件和修订，用户可从中签出任何文件的任何版本。 从远程 Subversion 存储库中签出文件时，用户将收到该时间点的存储库快照。

若要将 Subversion 用于版本控制，必须将其安装在计算机上。 若要检查计算机上是否已安装 Subversion，请在终端中使用以下命令：

```bash
svn --version
```

此命令返回版本号。

如果尚未安装 Subversion，要获取它的最简单方式是通过安装“Xcode 命令行工具”  。 使用以下命令安装 Xcode 命令行工具和 Subversion。

```bash
xcode-select --install
```

在计算机上安装 Subversion 后，使用以下步骤在 SVN 中发布项目。

1. 在线创建免费 SVN 存储库。 此示例中使用了 [Assembla](https://app.assembla.com/)。 创建后，将提供用于连接到此存储库的 URL：

    ![复制 SVN URL](media/version-control-subversion1-sml.png)

2. 打开或创建一个 Visual Studio for Mac 项目。

3. 右键单击该项目并选择“版本控制”>“在版本控制中发布...”  ：

    ![开始发布项目](media/version-control-subversion2.png)

4. 在“连接到存储库”选项卡中，从顶部下拉菜单中选择“Subversion”   。

5. 输入步骤 1 中获取的 URL。 输入 URL 后，默认将填充其他字段：

    ![选择“存储库”和“输入详细信息”对话框](media/version-control-subversion3.png)

7. 单击“确定”，然后按“发布”确认   。

7. 若出现提示，请为创建存储库的站点输入凭据，如下所示：

    ![输入 subversion 存储库的凭据](media/version-control-subversion5.png)

8. 现在，在版本控制菜单中，应可见所有可用的版本控制命令。

## <a name="see-also"></a>请参阅

- [使用 Subversion](working-with-subversion.md)