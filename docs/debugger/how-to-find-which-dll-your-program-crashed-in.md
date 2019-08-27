---
title: 如何：查找导致程序崩溃的 DLL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.dll
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, DLL crashes
- Module List dialog box
- errors [debugger], DLL crashes
- Modules window
- debugging [Visual Studio], DLL crashes
- DLLs, load order of
ms.assetid: ecf62568-8b65-4a41-b8a4-e962ff2dfb71
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b7a9421af9e0caf085feb1afb27b53befe837668
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894042"
---
# <a name="how-to-find-which-dll-your-program-crashed-in-c-c-visual-basic-f"></a>如何：查找导致程序崩溃的 DLL (C#， C++，Visual Basic 中， F#)

 如果应用程序在调用系统 DLL 或他人的代码时崩溃，则需要找出在崩溃发生时处于活动状态的 DLL。 如果在自己的程序之外的 DLL 中遇到崩溃，则可以使用**模块**窗口识别位置。

### <a name="to-find-where-a-crash-occurred-using-the-modules-window"></a>使用“模块”窗口查找崩溃发生的位置

1. 记下崩溃发生的地址。

    如果错误消息中未显示该地址，则可能需要使用其他方法来标识 DLL。 如果怀疑是系统 DLL ，则可以在调试时从 Microsoft Symbol Server [加载符号](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 否则，可能需要改用堆信息[创建转储文件](../debugger/using-dump-files.md)。 有多种[工具](https://blogs.msdn.microsoft.com/andrehal/2009/12/31/what-is-a-dump-and-how-do-i-create-one/)可用于创建转储文件。

2. 在“调试”菜单上，选择“Windows”，然后单击“模块”。

3. 在“模块”窗口中，找到“地址”列。 可能需要使用滚动条来查看。

4. 单击列顶部的“地址”按钮，按地址对 DLL 进行排序。

5. 细查排序的列表，找到其地址包含崩溃位置的 DLL。

6. 查看“名称”和“路径”列来查看 DLL 的名称和路径。

## <a name="see-also"></a>请参阅
- [调试 DLL 项目](../debugger/debugging-dll-projects.md)
- [如何：使用“模块”窗口](../debugger/how-to-use-the-modules-window.md)