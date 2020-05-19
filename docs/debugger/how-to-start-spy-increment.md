---
title: 如何：启动 Spy++ | Microsoft Docs
ms.date: 12/16/2018
ms.topic: conceptual
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70874d70dd5f845e7b627f2aeb7ae51bafe45995
ms.sourcegitcommit: 7b07e7b5e06e2e13f622445c568b78a284e1a40d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76542615"
---
# <a name="how-to-start-spy"></a>如何：启动 Spy++

可以从 Visual Studio 或在命令提示符处启动 Spy++。

 启动 Spy++ 时，如果显示消息以请求获得对计算机进行更改的权限，请选择“是”。

> [!NOTE]
> 只能运行 Spy++ 的一个实例。 如果尝试启动第二个实例，则只会导致当前正在运行的实例获得焦点。

## <a name="prerequisites"></a>先决条件

Spy++ 需要以下组件。 可以通过选择“单个组件”选项卡，然后选择以下组件，从 Visual Studio 安装程序中选择这些组件。

* 在“调试和测试”下，选择“C++ 分析工具”
* 在“开发活动”下，选择“C++ 核心功能”

如果进行了任何更改，请按照提示安装这些组件。

## <a name="start-spy-from-visual-studio"></a>从 Visual Studio 启动 Spy++

在“工具”菜单上选择“Spy++” 。

因为 Spy++ 独立运行，所以在启动之后，可以关闭 Visual Studio。

> [!NOTE]
> 使用 Spy++ 记录消息时，它可能会导致操作系统的执行速度变慢。

## <a name="start-spy-at-a-command-prompt"></a>在命令提示符处启动 Spy++

1. 在命令提示符窗口中，将目录更改为包含 spyxx.exe 的文件夹。 通常，此文件夹的路径为 ..\\Visual Studio 安装文件夹\Common7\Tools\\。

2. 输入 spyxx.exe。

## <a name="see-also"></a>请参阅
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)
