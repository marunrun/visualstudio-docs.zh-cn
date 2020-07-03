---
title: 如何 - 序列化符号信息 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VS.ToolsOptionsPages.Performance.General
helpviewer_keywords:
- profiling tools, serializing symbol information
- performance tools, serializing symbol information
ms.assetid: 9e0da706-6325-4073-83d1-aeab3b7c137a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d28df6d36b1b91974483ae793e6e57f064974183
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328526"
---
# <a name="how-to-serialize-symbol-information"></a>如何：序列化符号信息
可以序列化分析应用程序所需的符号。 符号序列化的作用是将符号添加到 .vsp 文件中。 通过向 .vsp 文件添加符号信息，其他人可以在没有原始符号访问权限的情况下分析性能报告。 如果未序列化符号，则需要有受检测的原始 .exe 和 .pdb 文件才能分析 .vsp 文件  。

### <a name="to-automatically-serialize-symbol-information"></a>自动序列化符号信息

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

     随即出现“选项”对话框。

2. 单击“性能工具”。

3. 在“常规设置”下，选择“自动序列化符号信息” 。

## <a name="see-also"></a>请参阅
- [配置性能会话](../profiling/configuring-performance-sessions.md)
- [如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)
- [如何：保存已分析的报告文件](/previous-versions/visualstudio/visual-studio-2010/bb763106\(v\=vs.100\))
