---
title: “调试会话的可执行文件”对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exefordebug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- executable files, specifying when debugging
- DLLs, debugging
- debugger, Executable for Debugging Session dialog box
- Executable for Debugging Session dialog box
ms.assetid: c0ddbe32-b99f-4425-acf1-f48842804f56
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 14d4ac95aae860e0750af66aec6adb2969434f11
ms.sourcegitcommit: ea182703e922c74725045afc251bcebac305068a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71211041"
---
# <a name="executable-for-debugging-session-dialog-box"></a>“调试会话的可执行文件”对话框

当您尝试调试没有指定可执行文件的 DLL 时，将出现该对话框。 Visual Studio 无法直接启动 DLL。 相反，Visual Studio 会启动指定的可执行文件。 可执行文件调用 DLL 时，可以对其进行调试。

 **可执行文件名称**输入调用要调试的 DLL 的可执行文件的路径名称。

 **可访问项目的 URL （仅限 ATL Server）** 如果正在调试 ATL Server DLL，请输入可在其中找到项目的 URL。

 输入后，这些设置将存储在项目属性页中，因此，以后调试会话时无需再次输入它们。 如果需要更改设置，您可以打开“属性页”并更改值。 有关为调试会话指定可执行文件的详细信息，请参阅[调试 DLL](../debugger/how-to-debug-from-a-dll-project.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)