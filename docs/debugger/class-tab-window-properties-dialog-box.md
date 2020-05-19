---
title: “窗口属性”对话框 ->“类别”选项卡 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, Class Tab
ms.assetid: eaec9f07-d580-436d-934d-76c4e59439aa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0917c9a038b42e6302ec1f1782f095ca397a92ef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62565008"
---
# <a name="class-tab-window-properties-dialog-box"></a>“窗口属性”对话框 ->“类”选项卡
使用“类别”选项卡可显示有关所选窗口类别的信息。 若要显示[窗口属性对话框](../debugger/window-properties-dialog-box.md)，将焦点移动到 [Windows 视图](../debugger/windows-view.md)窗口。 在树中选择任意窗口节点，然后从“视图”菜单选择“属性” 。

 “类别”选项卡中有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**类名**|此窗口类别的名称（或序号）。|
|**类样式**|类别样式代码的组合。|
|**类字节**|与此窗口类别关联的应用程序特定数据。|
|**类原子**|RegisterClass 调用返回的类别的原子。|
|**实例句柄**|注册该类别的模块的实例句柄。 实例句柄不是唯一的。|
|**窗口字节**|与此类别的每个窗口关联的额外字节数。 这些字节的含义由应用程序确定。 展开列表框可查看 DWORD 格式的字节值。|
|**窗口进程**|用于此类窗口的 WndProc 函数的当前地址。 它与“常规”选项卡上的“窗口进程”不同（如果窗口为子类）。|
|**菜单名称**|与此类窗口关联的主菜单的名称（如果没有菜单，则为“无”）。|
|**图标图柄**|与此类窗口关联的图标的句柄（如果没有图标，则为“无”）。|
|**游标图柄**|与此类窗口关联的光标的句柄（如果没有光标，则为“无”）。|
|**背景画笔**|与此类窗口关联的背景画笔的句柄，或用于绘制窗口背景的预定义 COLOR_* 颜色之一（如果没有画笔，则为“无”）。|