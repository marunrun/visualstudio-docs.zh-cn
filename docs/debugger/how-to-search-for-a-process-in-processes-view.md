---
title: 在进程视图中搜索进程 | Microsoft Docs
description: 在 Spy++ 工具的“进程”视图中搜索特定进程，方法是在 Visual Studio 中进行调试时，使用其进程 ID 或模块字符串作为搜索条件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f6c51276bea76fe77455d13e011aa85efa8f6fd
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98148554"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>如何：在进程视图中搜索进程
可以通过使用进程 ID 或模块字符串作为搜索条件，在进程视图中搜索特定进程。 还可以指定搜索的初始方向。 对话框中的字段将显示进程树中所选进程的属性。

### <a name="to-search-for-a-process-in-processes-view"></a>在进程视图中搜索进程

1. 排列窗口，以使 Spy++ 和活动的[进程视图](../debugger/processes-view.md)窗口可见。

2. 从“搜索”菜单中选择“查找进程”

    此时将打开[“进程搜索”对话框](../debugger/process-search-dialog-box.md)。

3. 键入进程 ID 或模块字符串作为搜索条件。

4. 清除任何不想为其指定值的字段。

   > [!TIP]
   > 若要查找模块拥有的所有进程，请清除“进程”框，然后在“模块”框中键入模块名称。 然后使用“查找下一个”继续搜索进程。

5. 选择“向上”或“向下”作为搜索的初始方向。

6. 单击 **“确定”** 。

   如果找到了匹配的进程，它会在 **进程视图** 窗口中突出显示。