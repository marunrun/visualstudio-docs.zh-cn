---
title: 停止在进度对话框中进行调试 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.stopnow
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Stop Debugging in Progress dialog box
ms.assetid: ed7ef49d-e25f-4a4d-9396-9bc7b4143117
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d3b2a3382fe9ac11f07d7fa9ebc5c1bc094cd526
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902499"
---
# <a name="stop-debugging-in-progress-dialog-box"></a>“停止正在进行的调试”对话框
当调试器尝试停止调试会话，但停止会话需要一段时间时，会出现此对话框。 停止调试会话通常很快，而此对话框并不出现。 但是，有时从正在调试的所有进程中分离需要额外的时间。 如果停止会话需要的时间超过几秒钟（或者发生分离错误），则会出现此对话框。 如果此对话框经常出现，则可能是由于内部问题，您可能需要与产品支持服务联系。

 可以等待进程分离，直到此对话框消失，或者使用“立即停止”按钮强制立即终止。

 **立即停止**单击此按钮可立即在调试会话结束。 使用**立即停止**将终止，而不是分离正在调试的进程。 如果正在调试系统进程，使用“立即停止”终止这些进程可能产生不希望出现的意外结果。

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [分离程序](/previous-versions/visualstudio/visual-studio-2010/x1thkxez(v=vs.100))