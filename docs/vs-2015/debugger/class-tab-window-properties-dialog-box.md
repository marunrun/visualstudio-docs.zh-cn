---
title: 类选项卡上，窗口属性对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Window Properties dialog box, Class Tab
ms.assetid: eaec9f07-d580-436d-934d-76c4e59439aa
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9a7f81a100b2c2311444732434df0f5c5599742a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161611"
---
# <a name="class-tab-window-properties-dialog-box"></a>“窗口属性”对话框 ->“类”选项卡
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用**类**选项卡以显示所选的窗口在类上的信息。 若要显示[窗口属性对话框](../debugger/window-properties-dialog-box.md)，将焦点移动到 [Windows 视图](../debugger/windows-view.md)窗口。 在树中选择任意窗口节点，然后从“视图”菜单选择“属性”   。  
  
 以下设置位于**类**选项卡：  
  
|条目|描述|  
|-----------|-----------------|  
|**类名**|此窗口类的名称 （或序号）。|  
|**类样式**|类样式代码的组合。|  
|**类字节**|与此窗口类关联的特定于应用程序的数据。|  
|**类原子**|类返回的 atom **RegisterClass**调用。|  
|**实例句柄**|注册此类模块的实例句柄。 实例句柄不是唯一的。|  
|**窗口字节**|与此类的每个窗口相关联的额外字节数。 这两个字节的含义取决于应用程序。 展开列表框中，若要查看 DWORD 格式的字节值。|  
|**窗口进程**|当前地址**WndProc**适用于 windows 的此类函数。 这不同于**窗口进程**上**常规**选项卡上，如果对窗口子类化。|  
|**菜单名称**|与此类 （如果没有菜单"无"） 的窗口相关联的主菜单的名称。|  
|**图标图柄**|与此类 （如果有任何图标"无"） 的窗口相关联的图标的句柄。|  
|**游标图柄**|与此类 （如果没有将游标"无"） 的 windows 光标的句柄。|  
|**背景画笔**|此类，或其中一个的预定义 COLOR_ * 颜色绘制窗口背景 （如果存在无画笔"无"） 的 windows 与相关联的背景画笔句柄。|
