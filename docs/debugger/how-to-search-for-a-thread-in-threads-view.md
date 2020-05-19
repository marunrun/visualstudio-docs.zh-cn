---
title: 如何：在线程视图中搜索线程 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- threads, searching
ms.assetid: 5609a9b3-c279-4426-9e2e-dd87896a6d6f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fd4014ca9eb99dce383b9de34e26794555b9fbef
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64798518"
---
# <a name="how-to-search-for-a-thread-in-threads-view"></a>如何：在线程视图中搜索线程
你可以使用线程 ID 或模块字符串作为搜索条件，在线程视图中搜索特定线程。 还可以指定搜索的初始方向。 此对话框中的字段将显示线程树中所选线程的属性。

### <a name="to-search-for-a-thread-in-threads-view"></a>在线程视图中搜索线程

1. 排列窗口，以使 Spy++ 和活动[线程视图](../debugger/threads-view.md)窗口可见。

2. 在“搜索”菜单中，选择“查找线程” 。

    [“线程搜索”对话框](../debugger/thread-search-dialog-box.md)随即打开。

3. 键入线程 ID 或模块字符串作为搜索条件。

4. 清除任何不想为其指定值的字段。

   > [!TIP]
   > 若要查找模块拥有的所有线程，请清除“线程”文本框，然后在“模块”框中键入模块名称 。 然后使用“查找下一个”继续搜索线程。

5. 选择“向上”或“向下”作为搜索的初始方向。

6. 单击 **“确定”** 。

   如果找到匹配的线程，它将在线程视图窗口中突出显示。