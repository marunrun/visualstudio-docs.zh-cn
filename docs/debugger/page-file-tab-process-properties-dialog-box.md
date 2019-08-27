---
title: 页面文件选项卡上，进程属性对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: daf41a06-8a55-48f6-95f5-49a8416bd308
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25dc3b0aca1b58c18ae4038540c14fc4dbfe4036
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62904102"
---
# <a name="page-file-tab-process-properties-dialog-box"></a>“进程属性”对话框 ->“页文件”选项卡
使用**页面文件**选项卡以查看进程的分页文件。 若要显示[“进程属性”对话框](../debugger/process-properties-dialog-box.md)，请将焦点移至[进程视图](../debugger/processes-view.md)窗口。 选择树中的任何进程节点，然后从“视图”菜单中选择“属性”。

 以下设置位于**页面文件**选项卡：

|条目|描述|
|-----------|-----------------|
|**页文件字节数**|此过程使用的分页文件中的页的数目。 分页文件存储过程使用的但不是包含其他文件中的数据的页。 分页文件由所有进程，并且当其他进程正在运行时，在分页文件的空间不足可能会导致错误。|
|**峰值页文件字节数**|此进程已在分页文件中使用最大页数。|
|**页面错误**|在此过程中执行的线程的页面错误数。 当线程引用不在其工作集中在主内存中的虚拟内存页面，页面错误时发生。 因此，页面将不从磁盘中检索它是否在备用列表上，因此已在主内存中，或如果它正由另一个处理与共享的页面。|