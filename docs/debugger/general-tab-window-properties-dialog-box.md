---
title: 常规选项卡，窗口属性对话框 |Microsoft 文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, General Tab
ms.assetid: 19142c60-9b32-46ba-a556-b62fd77568c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5160c79e2c8dae474927e6af7ebdc9e371e9edc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849564"
---
# <a name="general-tab-window-properties-dialog-box"></a>“窗口属性”对话框 ->“常规”选项卡
使用“常规”选项卡来显示所选窗口的信息。 若要显示[窗口属性对话框](../debugger/window-properties-dialog-box.md)，将焦点移动到 [Windows 视图](../debugger/windows-view.md)窗口。 在树中选择任意窗口节点，然后从“视图”菜单选择“属性”。 

 “常规”选项卡中有以下可用设置： 

|条目|描述|
|-----------|-----------------|
|**窗口标题**|中的文本窗口标题或包含在一个窗口，如果它是控件的文本。|
|**窗口句柄**|此窗口的唯一 ID。 重复使用窗口句柄号;它们仅对该窗口的生存期确定窗口。|
|**窗口进程**|此窗口的窗口过程函数虚拟地址。 此字段还指示此窗口是否是 Unicode 窗口，以及它是否子类化。|
|**矩形**|窗口边框。 此外会显示矩形的大小。 单位为像素屏幕坐标中。|
|**还原矩形**|还原窗口边框。 此外会显示矩形的大小。 仅在最大化或最小化窗口时，还原的矩形将不同于矩形。 单位为像素屏幕坐标中。|
|**客户端矩形**|窗口工作区的边框。 此外会显示矩形的大小。 单位为像素为单位的窗口工作区相对于左上角。|
|**实例句柄**|应用程序的实例句柄。 实例句柄不是唯一的。|
|**控件 ID 或菜单句柄**|如果要显示的窗口的子窗口，显示的控件 ID 标签。 控件 ID 是一个整数，用于标识此子窗口的控件 id。 如果要显示的窗口不是子窗口，显示的菜单处理标签。 菜单句柄是菜单的一个整数，用于标识与此窗口关联的句柄。|
|**用户数据**|附加到此窗口结构的特定于应用程序的数据。|
|**窗口字节**|与此窗口相关的额外字节数。 这两个字节的含义取决于应用程序。 展开列表框中，若要查看 DWORD 格式的字节值。|