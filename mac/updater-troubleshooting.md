---
title: 更新程序在检索信息时发生错误
description: 有关如何在看到错误“检索更新信息时出错”时进行修复的说明。 在 Visual Studio 2019 for Mac 中
author: asb3993
ms.author: amburns
ms.date: 04/13/2019
ms.technology: vs-ide-install
ms.assetid: 31AF914A-C66B-4CD3-9429-39695E0E94AE
ms.openlocfilehash: ef0d1f7516c410475f467ecaadecbb0aeaac71a3
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825715"
---
# <a name="troubleshooting-updater-has-errors-retrieving-information"></a>疑难解答：更新程序在检索信息时发生错误

在极少数情况下，可能会看到尝试[更新 Visual Studio for Mac](update.md) 时显示的错误消息“检索更新信息时出错”。 如果发生这种情况，请尝试执行以下步骤来修复此错误：

- 检查 Internet 连接。 连接中断是此错误的最常见原因。
  - 如果组件无法下载，则可以单击组件名称旁边的重试按钮以重新尝试下载。
- 重启 IDE。
- 如果此错误消息继续出现，也可以尝试使用安装程序进行更新，如果 .dmg  仍位于计算机上，也可以从 [my.visualstudio.com](https://visualstudio.microsoft.com/vs/mac/) 进行下载
  - 该安装程序将更新计算机上安装的任何组件。
  - 通过重新运行该安装程序，还可以安装之前未安装的任何缺失组件。
- 此外，还可以删除 `~/Library/Caches/VisualStudio/7.0/TempDownload/index.xml` 中的相应文件，来清除已缓存的下载。
