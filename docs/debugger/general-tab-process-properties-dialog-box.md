---
title: “进程属性”对话框 ->“常规”选项卡 | Microsoft Docs
description: 查看“常规”选项卡，了解有关进程的信息，包括模块名称、进程 ID、基本优先级、线程计数、CPU 时间、用户时间和运行时间。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: 86f4d61d-a594-4aac-8960-c5279b4a10fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4980437c63348050db1a007e8f541e9af9e186cc
ms.sourcegitcommit: 47da50a74fcd3db66d97cb20accac983bc41912f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96862732"
---
# <a name="general-tab-process-properties-dialog-box"></a>“进程属性”对话框 ->“常规”选项卡
使用“常规”选项卡详细了解特定进程。 若要显示[“进程属性”对话框](../debugger/process-properties-dialog-box.md)，请将焦点移动到[进程视图](../debugger/processes-view.md)窗口。 在树中选择任意进程节点，然后从“视图”菜单选择“属性” 。

 “常规”选项卡中有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**模块名**|模块的名称。|
|**进程 ID**|此进程的唯一 ID。 进程 ID 号是重复使用的，因此它们只在该进程的生存期内标识进程。 进程对象类型在程序运行时创建。 进程中的所有线程共享相同的地址空间，并且有权访问相同的数据。|
|**优先级基数**|此进程的当前基本优先级。 进程内的线程可以相对于进程的基本优先级提升和降低其自身的基本优先级。|
|**线程**|此进程中当前运行的线程数。|
|**CPU 时间**|此进程及其线程所用的总 CPU 时间。 等于用户时间加上特权时间。|
|**用户时间**|此进程的线程在非空闲线程中的用户模式下执行代码所用的累计时间。 应用程序在用户模式下执行，窗口管理器和图形引擎等子系统也是如此。|
|**特权时间**|此进程在非空闲线程的特权模式下运行的总运行时间。 服务层、执行例程和内核在特权模式下执行。 除图形适配器和打印机之外，大多数设备的设备驱动程序也在特权模式下执行。 除特权时间之外，Windows 对应用程序执行的一些工作可能会出现在其他子系统进程中。|
|**运行时间**|此进程已运行的总运行时间。|